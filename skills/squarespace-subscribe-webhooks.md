---
name: squarespace-subscribe-webhooks
description: >-
  Register a Squarespace webhook subscription, verify the HMAC-SHA256 Squarespace-Signature on
  every delivery, rotate the signing secret, and send a test notification — the OAuth-only path
  from polling to event-driven.
api: Squarespace Commerce API
version: '1.0'
base_url: https://api.squarespace.com
operations:
  - createWebhookSubscription
  - getWebhookSubscriptions
  - getWebhookSubscription
  - updateWebhookSubscription
  - deleteWebhookSubscription
  - rotateSubscriptionSecret
  - sendTestNotificationForWebhookSubscription
generated: '2026-08-13'
method: generated
source: openapi/squarespace-commerce-api-v2-openapi.json
---

# Subscribe to Squarespace webhooks

## Read this first: API keys will not work

The Webhook Subscriptions API is **OAuth only**. There is no API-key permission for it. If you try
with a Developer API Key you get `403` with subtype `OAUTH_TOKEN_REQUIRED`. You need a registered
Squarespace OAuth client (an Extension) and an access token.

Order events additionally require the Commerce **Orders** OAuth permission; contact and address
events require the **Contacts** permission.

## Steps

### 1. Create the subscription

`createWebhookSubscription` — `POST /1.0/webhook_subscriptions`

Body: your `endpointUrl` and the `topics[]` you want.

Available topics, from the provider's catalog:

| Family | Topics |
|---|---|
| Extension | `extension.uninstall` |
| Orders | `order.create`, `order.update` |
| Contacts | `contact.create`, `contact.update`, `contact.delete` |
| Address book | `address.create`, `address.update`, `address.delete` |

**Capture `secret` from this response and store it now.** It is returned *only* here and on a
secret rotation. There is no read-back operation for it. Losing it means you cannot verify
signatures and your only recovery is a rotation.

Subscriptions **never expire**.

### 2. Verify every delivery

Squarespace POSTs to your endpoint with:

- `User-Agent: Squarespace/1.0`
- `Content-Type: application/json`
- `Squarespace-Signature: <HMAC-SHA256>`

Compute HMAC-SHA256 over the raw request body using the subscription `secret` and compare in
constant time. Reject anything that does not match — an unverified endpoint is an open write path
into your system.

The payload envelope is always:

```json
{
  "id": "5c2ba184b63ed3cb411ce2b1",
  "websiteId": "5f3c3d55ac435e1a051f77b3",
  "subscriptionId": "5f3c2155d947844beedda991",
  "topic": "extension.uninstall",
  "createdOn": "2020-04-22T22:18+00:00",
  "data": { }
}
```

`data` is topic-specific. **Squarespace reserves the right to add properties and fields to this
payload without a version change** — version changes are reserved for breaking changes only. Parse
permissively.

### 3. Test before you trust

`sendTestNotificationForWebhookSubscription` —
`POST /1.0/webhook_subscriptions/{subscriptionId}/actions/sendTestNotification`

Use this to prove your endpoint is reachable and your signature check accepts a genuine Squarespace
delivery, before any real event depends on it.

### 4. Rotate the secret

`rotateSubscriptionSecret` —
`POST /1.0/webhook_subscriptions/{subscriptionId}/actions/rotateSecret`

Returns a new `secret`. There is no published overlap window in which both the old and new secret
verify, so treat rotation as a cutover: rotate, store, and be ready to accept a brief window of
signature failures — or accept both secrets in your verifier across the rotation.

### 5. Manage the set

- `getWebhookSubscriptions` — `GET /1.0/webhook_subscriptions`
- `getWebhookSubscription` — `GET /1.0/webhook_subscriptions/{subscriptionId}`
- `updateWebhookSubscription` — `POST /1.0/webhook_subscriptions/{subscriptionId}` (note: **POST**,
  not PUT or PATCH)
- `deleteWebhookSubscription` — `DELETE /1.0/webhook_subscriptions/{subscriptionId}`

`409 WEBHOOK_SUBSCRIPTION_LIMIT_REACHED` means the site is at its subscription cap; delete an unused
subscription rather than retrying.

## The Payment Plans trap

For a Payment Plan order, `order.create` fires **only when `paymentState` transitions to `PAID`** —
that is, when every installment has been collected — not when the shopper places the order. This was
done deliberately to preserve backward compatibility for existing integrations.

If your fulfilment depends on knowing about the order at purchase time, webhooks alone will not tell
you. Poll `getOrders` with `paymentStates=PARTIALLY_PAID` to see payment-plan orders that are still
collecting.

## Migrating off polling

The whole point of this flow is to stop crawling `getOrders`. But note what has no webhook: there
are **no product, inventory, discount or transaction events**. Anything outside orders, contacts and
addresses still requires polling against the 300/minute limit.
