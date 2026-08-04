# Squarespace (squarespace)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Squarespace is an all-in-one website building and e-commerce platform that enables individuals and businesses to create, manage, and scale their online presence. Squarespace provides a suite of Commerce APIs for developers to build integrations managing products, orders, inventory, customer profiles, transactions, and webhook notifications. All APIs use HTTPS REST conventions with API key or OAuth authentication.

**APIs.json:** [https://www.squarespace.com](https://www.squarespace.com)

## Tags

- Commerce
- E-Commerce
- Marketing
- Payments
- Retail
- Website Builder
- Webhooks

## Timestamps

- **Created:** 2026-05-02
- **Modified:** 2026-05-19

## APIs

### Squarespace Commerce API

The Squarespace Commerce API provides programmatic access to the commerce features of a Squarespace merchant site. It enables developers to manage products, process orders, track inventory, access customer profiles, retrieve financial transactions, and configure webhook subscriptions. All endpoints use HTTPS and follow REST principles.

#### Tags

- Commerce
- E-Commerce
- REST API

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/overview)
- [OpenAPI](openapi/squarespace-commerce-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-commerce-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-commerce-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Authentication](https://developers.squarespace.com/commerce-apis/making-requests)
- [Spectral Rules](rules/squarespace-rules.yml)
- [JSON-LD](json-ld/squarespace-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Vocabulary](vocabulary/squarespace-vocabulary.yml)

### Squarespace Orders API

The Squarespace Orders API provides access to order history for a Squarespace merchant site, supporting both one-time purchases and subscription orders. Developers can retrieve, create, and manage orders, as well as import orders from third-party sales channels into Squarespace.

#### Tags

- Commerce
- Orders
- REST API

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/orders-overview)
- [OpenAPI](openapi/squarespace-orders-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-orders-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-orders-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Squarespace Products API

The Squarespace Products API allows developers to manage the product catalog of a Squarespace merchant site. It supports physical products, service products, gift cards, and digital downloads, along with their images and variants.

#### Tags

- Commerce
- Products
- REST API

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/products-overview)
- [OpenAPI](openapi/squarespace-products-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-products-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-products-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Squarespace Inventory API

The Squarespace Inventory API enables developers to retrieve and update inventory quantities for product variants on a Squarespace merchant site. It supports bulk inventory queries and individual variant stock management.

#### Tags

- Commerce
- Inventory
- REST API

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/inventory-overview)
- [OpenAPI](openapi/squarespace-inventory-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-inventory-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-inventory-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Squarespace Profiles API

The Squarespace Profiles API allows reading customer profiles, mailing list subscribers, and donors for a Squarespace site. It supports filtering by profile type and retrieving individual profile details.

#### Tags

- CRM
- Customer Profiles
- REST API

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/profiles-overview)
- [OpenAPI](openapi/squarespace-profiles-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-profiles-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-profiles-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Squarespace Transactions API

The Squarespace Transactions API provides access to financial transaction records for a Squarespace merchant site. Developers can retrieve transaction history, including payment amounts, fees, and associated order or subscription references.

#### Tags

- Commerce
- Finance
- Transactions

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/transactions-overview)
- [OpenAPI](openapi/squarespace-transactions-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-transactions-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-transactions-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Squarespace Webhook Subscriptions API

The Squarespace Webhook Subscriptions API allows developers to manage webhook endpoint subscriptions for a merchant site. It supports creating, listing, updating, and deleting subscriptions that trigger notifications for order events, extension uninstalls, and other commerce activities.

#### Tags

- Webhooks
- Event Notifications
- REST API

#### Properties

- [Documentation](https://developers.squarespace.com/webhooks/overview)
- [OpenAPI](openapi/squarespace-webhook-subscriptions-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/squarespace-webhook-subscriptions-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/squarespace-webhook-subscriptions-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [AsyncAPI](asyncapi/squarespace-webhooks-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/latest)

## Common Properties

- [GitHub Organization](https://github.com/squarespace)
- [LinkedIn](https://www.linkedin.com/company/squarespace)
- [Website](https://www.squarespace.com)
- [Developer Portal](https://developers.squarespace.com)
- [Documentation](https://developers.squarespace.com/commerce-apis/overview)
- [A P I Keys](https://support.squarespace.com/hc/en-us/articles/236297987-Squarespace-API-keys)
- [Terms of Service](https://www.squarespace.com/terms-of-service)
- [Privacy Policy](https://www.squarespace.com/privacy)
- [Status Page](https://status.squarespace.com)
- [Blog](https://www.squarespace.com/blog)

## Maintainers

**URL:** https://developers.squarespace.com
