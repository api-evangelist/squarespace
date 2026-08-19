---
name: squarespace-import-order
description: >-
  Import an order from a third-party sales channel into a Squarespace merchant site safely, using
  the required Idempotency-Key so a retry can never create a duplicate order, then verify the
  result and read back the financial record.
api: Squarespace Commerce API
version: '2'
base_url: https://api.squarespace.com
operations:
  - createOrder
  - getOrder
  - getOrders
  - getDocumentsByUpdatedOn
generated: '2026-08-13'
method: generated
source: openapi/squarespace-commerce-api-v2-openapi.json
---

# Import an order into Squarespace

Use this when an order was placed somewhere else — a marketplace, a POS, another storefront — and
the merchant needs it to exist in Squarespace.

## Before you start

- **Credential.** `Authorization: Bearer <API key or OAuth token>`. An API key needs the **Orders**
  permission at Read and Write. API keys require the merchant to be on the Squarespace Advanced plan.
- **User-Agent is mandatory.** A request with no `User-Agent` header is rejected outright. Send a
  descriptive one; a default client string (`curl/7.54.0`) is accepted but may be rate-limited harder.
- **This operation is API-key rate-limited to 100 requests per hour, per website.** OAuth-
  authenticated callers are exempt from that cap and fall back to the global 300/minute. If you are
  bulk-importing, use OAuth.

## Steps

### 1. Generate an idempotency key and create the order

`createOrder` — `POST /1.0/commerce/orders`

The `Idempotency-Key` header is **required**, not optional. Generate one key per logical order —
a UUID is fine — and reuse that same key for every retry of that same order.

```
POST https://api.squarespace.com/1.0/commerce/orders
Authorization: Bearer <token>
User-Agent: <your app>
Content-Type: application/json
Idempotency-Key: 6b1f0c2e-9a44-4f1a-8f0e-2f1d3c4b5a60
```

The body is a `CreateOrderRequest`: `channelName`, `externalOrderReference`, `customerEmail`,
`billingAddress`, `shippingAddress`, `lineItems[]` (`CreateLineItemRequest`), `shippingLines[]`,
`discountLines[]`, `priceTaxInterpretation`, `subtotal`, `shippingTotal`, `discountTotal`,
`taxTotal`, `grandTotal`, `fulfillmentStatus`, and `inventoryBehavior`.

Two fields decide behaviour and are easy to get wrong:

- **`inventoryBehavior`** (`CreateOrderInventoryBehavior`) controls whether the import decrements
  Squarespace stock. Set it deliberately — an import from a channel that already decremented its own
  stock should usually not decrement again.
- **Money must agree.** `grandTotal` has to reconcile with the line items, shipping, discounts and
  tax you supplied. A mismatch is a `400 INVALID_REQUEST_ERROR`. Every amount is a `MonetaryAmount`
  and every currency must match the site currency, or you get subtype `CURRENCY_MISMATCH`.
- **Price ceilings are per-currency.** 1,000,000 for most currencies; 999,999,999 JPY,
  99,999,999 KRW, 10,000,000 HUF and COP.

### 2. Handle the response honestly

- `201` — the order was created and is in the body. Store the returned `id`.
- Same key, same parameters, retried — you get the **same response back**, and no second order is
  created. Keys are guaranteed effective for **48 hours**.
- `409 CONFLICT` — most often `INSUFFICIENT_STOCK` or `CONCURRENT_MODIFICATION`. Do **not** blind-
  retry a 409. Re-read state first, then decide.
- `429` — wait a flat **one minute**. Squarespace publishes no `Retry-After` and no `RateLimit-*`
  headers, so the back-off has to be hard-coded.
- `402 WEBSITE_EXPIRED` — the merchant's Squarespace billing has lapsed. Not retryable by you;
  surface it to the merchant.
- `5xx` — retry with exponential backoff, bounded. Keep the same `Idempotency-Key`. Capture the
  `contextId` from the error body; Squarespace requires it on any support report.

### 3. Verify the order landed

`getOrder` — `GET /1.0/commerce/orders/{id}`

Confirm `paymentState` and `fulfillmentStatus` are what you expect. `paymentState` is the canonical
payment status (added 2026-05-08); do not infer payment status from transactions.

### 4. Reconcile the money

`getDocumentsByUpdatedOn` — `GET /1.0/commerce/transactions?orderId={id}`

The Transactions `Document` carries one `TransactionPayment` per captured payment. For a Payment
Plan order the deposit lands first and installments accumulate over time, so a document with fewer
payments than expected is not necessarily an error.

## Finding an already-imported order

`getOrders` — `GET /1.0/commerce/orders`

Filter with `customerId`, `fulfillmentStatus`, `paymentStates`, or the `modifiedAfter` /
`modifiedBefore` pair. **Those two are mutually required** — passing one without the other is a
400. Neither can be combined with `cursor`.

Paging is cursor-based, 50 per page, via `pagination.nextPageCursor`. Squarespace cursors are
*dynamic*: they point at a position, not a snapshot. If orders are being created while you page,
the result set shifts under you. For a reconciliation run, prefer a bounded
`modifiedAfter`/`modifiedBefore` window over an open-ended crawl.

## What this skill will not do

There is no Squarespace-operated MCP tool for orders. This flow is REST-only.
