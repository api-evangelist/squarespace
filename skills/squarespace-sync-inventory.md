---
name: squarespace-sync-inventory
description: >-
  Reconcile stock levels between an external system of record and a Squarespace merchant site —
  walk the product catalog to variant IDs, read current stock, and apply adjustments with the
  required Idempotency-Key so a retried sync cannot double-count.
api: Squarespace Commerce API
version: '2'
base_url: https://api.squarespace.com
operations:
  - getProducts
  - getSpecificProducts
  - getInventoryItems
  - getSpecificInventoryItems
  - adjustInventoryStockLevels
generated: '2026-08-13'
method: generated
source: openapi/squarespace-commerce-api-v2-openapi.json
---

# Sync inventory with Squarespace

## The one structural fact to internalise

**Inventory has no identity of its own.** An `InventoryItem` is keyed by `variantId` — there is no
inventory ID, and no way to ask "what is the stock for this product". Every inventory operation
starts from a product variant. If you do not already hold variant IDs, step 1 is not optional.

## Before you start

- **Credential.** `Authorization: Bearer <token>` with the **Inventory** permission at Read and
  Write for adjustments, plus **Products** read to resolve variants.
- **`User-Agent` is required** or the request is rejected.
- Global limit: 300 requests/minute (5/second). On `429`, wait one minute — there is no
  `Retry-After` header to read.

## Steps

### 1. Resolve variant IDs from the catalog

`getProducts` — `GET /v2/commerce/products`

Page with `cursor` (50 per page, `pagination.nextPageCursor`). Each `ProductV2` carries
`variants[]`, and each `ProductVariantV2` has the `id` you need. Note:

- Download products have **no variants** and no stock.
- `type` filters the list to `PHYSICAL`, `SERVICE`, `GIFT_CARD` or `DIGITAL`.

If you already know the products, `getSpecificProducts` —
`GET /v2/commerce/products/{productIdCsvs}` — takes a **comma-separated list in the path**, not a
query parameter. That is the cheap path and worth preferring.

### 2. Read current stock

`getInventoryItems` — `GET /1.0/commerce/inventory` walks everything, cursor-paged.

`getSpecificInventoryItems` — `GET /1.0/commerce/inventory/{variantIdCsvs}` reads a known set, again
comma-separated in the path. Use this when you are reconciling a known SKU list; it is far fewer
calls than a full crawl.

Each `InventoryItem` carries `variantId`, `sku`, `descriptor`, `isUnlimited` and `quantity`.
**Check `isUnlimited` before you compute anything** — an untracked variant will reject adjustments
with subtype `STOCK_NOT_TRACKED`.

### 3. Apply the adjustment

`adjustInventoryStockLevels` — `POST /1.0/commerce/inventory/adjustments`

The `Idempotency-Key` header is **required**. This is the operation the header exists for: an
adjustment is a delta, so a retry without a key double-applies it and silently corrupts the
merchant's stock.

```
POST https://api.squarespace.com/1.0/commerce/inventory/adjustments
Authorization: Bearer <token>
User-Agent: <your app>
Content-Type: application/json
Idempotency-Key: 2c9a7e51-33f0-4bd6-9f4d-0a7e1c2b3d44
```

Body is a `CreateInventoryAdjustmentRequest`. Generate **one key per adjustment batch** and hold it
across every retry of that batch. Keys may be up to 64 characters (alphanumeric, dashes,
underscores; UUIDs are conventional) and are guaranteed effective for 48 hours.

### 4. Read the errors correctly

- `409 INSUFFICIENT_STOCK` — the adjustment would take quantity below zero.
- `409 STOCK_EXCEEDS_MAX` — above the permitted ceiling.
- `409 STOCK_NOT_TRACKED` — the variant is unlimited; there is nothing to adjust.
- `409 CONCURRENT_MODIFICATION` — another writer touched the same variant. Re-read and recompute;
  do not blind-retry.
- `404 INVENTORY_ITEM_NOT_FOUND` / `PRODUCT_VARIANT_NOT_FOUND` — the variant ID is stale. Re-resolve
  from the catalog; variants are deleted when a merchant edits a product.
- `403 MISSING_SCOPE` — the key or token has Inventory read-only. Permissions on an issued
  credential **cannot be changed**; a new key must be generated, or the merchant must re-authorize.

## Sync design notes

- Cursors are **dynamic**, not snapshots. A catalog crawl that runs while the merchant is editing
  products will see a shifting result set. For a nightly reconciliation, crawl to a variant-ID list
  first, then read and adjust against that fixed list.
- Squarespace ships additive response changes without a version bump, so your deserializer must
  tolerate new fields. Array fields may come back as `null` **or** `[]` — handle both.
- There is no bulk "set stock to N" operation. Everything is an adjustment relative to current
  quantity, which is exactly why step 2 must precede step 3.
