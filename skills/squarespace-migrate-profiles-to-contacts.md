---
name: squarespace-migrate-profiles-to-contacts
description: >-
  Move an integration off the maintenance-mode Squarespace Profiles API onto the Contacts API —
  read the legacy records, map the two incompatible address shapes, and adopt the write, query and
  webhook capabilities Profiles never had.
api: Squarespace Commerce API
version: v1
base_url: https://api.squarespace.com
operations:
  - getProfiles
  - getSpecificProfiles
  - getContacts
  - queryContacts
  - getContact
  - createContact
  - patchContact
  - getAddressBook
  - createAddressBookEntry
  - getTransactionsSummaries
generated: '2026-08-13'
method: generated
source: openapi/squarespace-commerce-api-v2-openapi.json
---

# Migrate from Profiles to Contacts

## Why

On 2026-04-09 Squarespace shipped the Contacts API and put the Profiles API into **maintenance
mode**. Its own guidance: migration is "highly recommended" and new integrations should use Contacts.

Two things about that deprecation matter operationally:

1. **No sunset date has been published.** The policy says "extended period" and "significant advance
   notice" without a number. Profiles still works today.
2. **The contract does not carry the deprecation.** Zero of the 55 published operations are marked
   `deprecated: true`, including both Profiles operations, and no `Sunset` or `Deprecation` response
   header is emitted. Nothing in the machine-readable surface or the wire protocol will warn you.
   The changelog is the only signal.

Write behaviour on Profiles was already restricted to allowed developers back in 2021, so for most
integrations Profiles has been read-only for years.

## What you gain

| Capability | Profiles | Contacts |
|---|---|---|
| Read | yes | yes |
| Create / update / delete | no | yes |
| Address book management | no | yes, up to 50 per contact |
| Query / filter | no | yes, `POST /v1/contacts/query` |
| Webhooks | no | yes, `contact.*` and `address.*` |
| API key auth | yes | yes, since 2026-06-17 |

## Steps

### 1. Inventory what you have

`getProfiles` — `GET /1.0/profiles`, cursor-paged.
`getSpecificProfiles` — `GET /1.0/profiles/{profileIdCsvs}` for a known set.

A `Profile` carries `id`, name, email, `address` (an `Address`), marketing preferences and
`transactionsSummary`.

### 2. Map the fields — and watch the address shape

This is the one genuinely dangerous part of the migration. **Profiles and Contacts do not share an
address type.**

- `Profile.address` is an `Address` — the same shape used by `Order.billingAddress`.
- `Contact` has no inline address at all. Addresses live in a separate address book, and each
  `AddressBookEntry.address` is a **`ContactAddress`** — a different schema.

Do not assume field-for-field compatibility. Map explicitly and test with real data.

Other mappings:

- `Profile.transactionsSummary` has no equivalent field on `Contact`. The replacement is the
  Analytics API: `getTransactionsSummaries` — `POST /v1/analytics/transaction-summaries` — which
  returns aggregated order counts, totals and donations for contacts **in bulk**. This is better than
  what Profiles gave you, but it is a separate call.
- Marketing preferences move to `Contact.acceptsMarketing` / `AcceptsMarketingWithDate`. Writing a
  marketing opt-in to a contact that cannot accept it returns subtype
  `PROFILE_CANNOT_ACCEPT_MARKETING`.
- `Contact.primaryEmail` is an `Email` object, not a bare string.

**Identifiers do not carry over.** Both are 24-character hex IDs with no type prefix, and nothing in
the contract maps a `Profile.id` to a `Contact.id`. Match on email and keep your own crosswalk table.

### 3. Read the new surface

`getContacts` — `GET /v1/contacts`, cursor-paged.

`queryContacts` — `POST /v1/contacts/query` for anything that will not fit in a query string: search
by name or email, filter by marketing status, order history or donation activity.

`getContact` — `GET /v1/contacts/{contactId}`.
`getAddressBook` — `GET /v1/contacts/{contactId}/address-book`.

### 4. Start writing

`createContact` — `POST /v1/contacts`
`patchContact` — `PATCH /v1/contacts/{contactId}` (a real PATCH — unusual in this API, where most
updates are POST)
`createAddressBookEntry` — `POST /v1/contacts/{contactId}/address-book`

`409 DUPLICATE_USER_CONFLICT` means a contact with that email already exists — read it and patch
rather than retrying the create.

### 5. Swap polling for events

Register `contact.create`, `contact.update`, `contact.delete`, `address.create`, `address.update`
and `address.delete` — see the `squarespace-subscribe-webhooks` skill. Profiles had no events, so
this is the largest practical gain from the migration.

## Auth changes

Contacts launched OAuth-only on 2026-04-09 and gained API-key support on 2026-06-17. If your
integration uses an API key, generate a new one with the **Contacts** permission — permissions on an
existing key cannot be modified. OAuth clients need the `website.contacts` or `website.contacts.read`
scope, and the merchant must re-initiate the connection to grant it.

## Version note

Profiles is `/1.0/profiles`; Contacts is `/v1/contacts`. These are different versioning eras, not
consecutive versions — pre-2025 Squarespace used `Major.Minor` SemVer, and from 2025 it uses plain
integers. Do not read `1.0` → `v1` as an upgrade path.
