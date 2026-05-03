# Squarespace

Squarespace is an all-in-one website building and e-commerce platform that enables individuals and businesses to create, manage, and scale their online presence. Squarespace provides a suite of Commerce APIs for developers to build integrations managing products, orders, inventory, customer profiles, transactions, and webhook notifications.

**Website:** [squarespace.com](https://www.squarespace.com)
**Developer Portal:** [developers.squarespace.com](https://developers.squarespace.com)
**Documentation:** [Commerce APIs Overview](https://developers.squarespace.com/commerce-apis/overview)

## APIs

| API | Description | OpenAPI |
|---|---|---|
| Commerce API | Master Commerce API covering all commerce capabilities | [openapi](openapi/squarespace-commerce-api-openapi.yml) |
| Orders API | Order history, creation, and fulfillment management | [openapi](openapi/squarespace-orders-api-openapi.yml) |
| Products API | Product catalog management with variants and images | [openapi](openapi/squarespace-products-api-openapi.yml) |
| Inventory API | Stock level retrieval and adjustment | [openapi](openapi/squarespace-inventory-api-openapi.yml) |
| Profiles API | Customer, subscriber, and donor profile access | [openapi](openapi/squarespace-profiles-api-openapi.yml) |
| Transactions API | Financial transaction records and reporting | [openapi](openapi/squarespace-transactions-api-openapi.yml) |
| Webhook Subscriptions API | Real-time event notification management | [openapi](openapi/squarespace-webhook-subscriptions-api-openapi.yml) |

## Artifacts

### OpenAPI Specifications

- [squarespace-commerce-api-openapi.yml](openapi/squarespace-commerce-api-openapi.yml) — Commerce API overview and site information
- [squarespace-orders-api-openapi.yml](openapi/squarespace-orders-api-openapi.yml) — Orders retrieval, creation, and fulfillment
- [squarespace-products-api-openapi.yml](openapi/squarespace-products-api-openapi.yml) — Product catalog CRUD with variants and images
- [squarespace-inventory-api-openapi.yml](openapi/squarespace-inventory-api-openapi.yml) — Stock level retrieval and bulk adjustment
- [squarespace-profiles-api-openapi.yml](openapi/squarespace-profiles-api-openapi.yml) — Customer and subscriber profile access
- [squarespace-transactions-api-openapi.yml](openapi/squarespace-transactions-api-openapi.yml) — Financial transaction records
- [squarespace-webhook-subscriptions-api-openapi.yml](openapi/squarespace-webhook-subscriptions-api-openapi.yml) — Webhook subscription CRUD and test notifications

### AsyncAPI Specifications

- [squarespace-webhooks-asyncapi.yml](asyncapi/squarespace-webhooks-asyncapi.yml) — Webhook event notification schemas (order.create, order.update, extension.uninstall)

### Spectral Rules

- [squarespace-rules.yml](rules/squarespace-rules.yml) — Spectral ruleset enforcing Squarespace API conventions: cursor pagination, bearer auth, Title Case summaries, JSON content types

### Naftiko Capabilities

- [commerce-management.yaml](capabilities/commerce-management.yaml) — Unified commerce management: Orders + Products + Inventory (REST + MCP)
- [customer-and-reporting.yaml](capabilities/customer-and-reporting.yaml) — Customer and reporting: Profiles + Transactions + Webhooks (REST + MCP)

#### Shared Per-API Definitions

- [orders.yaml](capabilities/shared/orders.yaml) — Squarespace Orders API shared definition
- [products.yaml](capabilities/shared/products.yaml) — Squarespace Products API shared definition
- [inventory.yaml](capabilities/shared/inventory.yaml) — Squarespace Inventory API shared definition
- [transactions.yaml](capabilities/shared/transactions.yaml) — Squarespace Transactions API shared definition
- [profiles.yaml](capabilities/shared/profiles.yaml) — Squarespace Profiles API shared definition
- [webhook-subscriptions.yaml](capabilities/shared/webhook-subscriptions.yaml) — Squarespace Webhook Subscriptions API shared definition

### JSON Schema

- [squarespace-order-schema.json](json-schema/squarespace-order-schema.json) — Schema for Squarespace order objects
- [squarespace-product-schema.json](json-schema/squarespace-product-schema.json) — Schema for Squarespace product objects
- [squarespace-webhook-notification-schema.json](json-schema/squarespace-webhook-notification-schema.json) — Schema for webhook event notification payloads

### JSON Structure

- [squarespace-order-structure.json](json-structure/squarespace-order-structure.json) — Field documentation for order objects
- [squarespace-product-structure.json](json-structure/squarespace-product-structure.json) — Field documentation for product objects

### JSON-LD

- [squarespace-context.jsonld](json-ld/squarespace-context.jsonld) — JSON-LD context for Squarespace commerce vocabulary

### Examples

- [squarespace-list-orders-example.json](examples/squarespace-list-orders-example.json) — List orders with status and date filters
- [squarespace-list-products-example.json](examples/squarespace-list-products-example.json) — List physical products with variant details

### Vocabulary

- [squarespace-vocabulary.yml](vocabulary/squarespace-vocabulary.yml) — Squarespace domain vocabulary: orders, products, variants, inventory, profiles, transactions, webhooks, cursors, HMAC

## Authentication

All Commerce APIs use Bearer token authentication:

```
Authorization: Bearer YOUR_API_KEY
```

API keys are generated from the Squarespace account settings. Webhook subscriptions require OAuth 2.0 token authentication.

## Common Properties

- [Developer Portal](https://developers.squarespace.com)
- [API Keys](https://support.squarespace.com/hc/en-us/articles/236297987-Squarespace-API-keys)
- [Terms of Service](https://www.squarespace.com/terms-of-service)
- [Privacy Policy](https://www.squarespace.com/privacy)
- [Status Page](https://status.squarespace.com)

## Tags

Commerce, E-Commerce, Marketing, Payments, Retail, Website Builder, Webhooks
