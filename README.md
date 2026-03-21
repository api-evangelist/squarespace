# Squarespace (squarespace)
Squarespace is a website building and e-commerce platform that enables businesses and individuals to create and manage online stores, portfolios, and websites. Through the Squarespace Developer Platform, developers can access a suite of Commerce APIs for managing products, orders, inventory, customers, transactions, and webhooks, as well as tools for building custom templates and OAuth-based integrations.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/squarespace/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags:

 - E-Commerce, Commerce, Website Builder, Orders, Products, Inventory, Webhooks, OAuth

## Timestamps

- **Created:** 2026-03-21
- **Modified:** 2026-03-21

## APIs

### Squarespace Commerce API
The Squarespace Commerce API provides programmatic access to the commerce features of a Squarespace merchant site. It enables developers to build integrations and applications that manage products, process orders, track inventory, access customer profiles, retrieve financial transactions, and configure webhook subscriptions. All endpoints use HTTPS and follow REST principles with standard verbs and response status codes. Authentication is handled via API keys or OAuth tokens, allowing both personal and third-party application access to merchant data.

**Human URL:** [https://developers.squarespace.com/commerce-apis/overview](https://developers.squarespace.com/commerce-apis/overview)


#### Tags:

 - Commerce, E-Commerce, Website Builder, Retail

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/overview)
- [OpenAPI](openapi/squarespace-commerce-api-openapi.yml)

### Squarespace Orders API
The Squarespace Orders API provides access to order history for a Squarespace merchant site, supporting both one-time purchases and subscription orders. Developers can retrieve, create, and manage orders, as well as import orders from third-party sales channels into Squarespace. The API supports filtering and pagination for retrieving large sets of orders. It is commonly used to synchronize order data with external fulfillment systems, ERPs, or custom reporting tools.

**Human URL:** [https://developers.squarespace.com/commerce-apis/orders-overview](https://developers.squarespace.com/commerce-apis/orders-overview)


#### Tags:

 - Orders, Commerce, E-Commerce, Fulfillment

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/orders-overview)
- [OpenAPI](openapi/squarespace-orders-api-openapi.yml)

### Squarespace Inventory API
The Squarespace Inventory API enables reading and adjusting stock information for product variants on a Squarespace merchant site. Developers can retrieve current inventory levels and apply incremental adjustments to stock quantities. This API is useful for integrating Squarespace with warehouse management systems, point-of-sale systems, or multi-channel inventory management platforms. Inventory adjustments can be applied in bulk across multiple product variants.

**Human URL:** [https://developers.squarespace.com/commerce-apis/inventory-overview](https://developers.squarespace.com/commerce-apis/inventory-overview)


#### Tags:

 - Inventory, Commerce, Stock Management, E-Commerce

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/inventory-overview)
- [OpenAPI](openapi/squarespace-inventory-api-openapi.yml)

### Squarespace Products API
The Squarespace Products API allows developers to manage the product catalog of a Squarespace merchant site. It supports physical products, service products, gift cards, and digital downloads, along with their images and variants. Developers can create, update, retrieve, and delete products programmatically, enabling catalog synchronization with external systems. The API is well-suited for building product import tools, headless commerce integrations, or multi-channel retail management applications.

**Human URL:** [https://developers.squarespace.com/commerce-apis/products-overview](https://developers.squarespace.com/commerce-apis/products-overview)


#### Tags:

 - Products, Commerce, Catalog, E-Commerce

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/products-overview)
- [OpenAPI](openapi/squarespace-products-api-openapi.yml)

### Squarespace Profiles API
The Squarespace Profiles API provides access to Profile resource objects, representing customers, mailing list subscribers, and donors associated with a Squarespace site. Each profile includes contact information, an approximate address derived from existing data, and a summary of the user's commerce activity such as orders and donations. This API is useful for CRM integrations, email marketing platforms, and customer analytics tools. Profile data is generated asynchronously from site activity and accessible through the standard Profiles panel.

**Human URL:** [https://developers.squarespace.com/commerce-apis/profiles-overview](https://developers.squarespace.com/commerce-apis/profiles-overview)


#### Tags:

 - Profiles, Customers, Commerce, CRM

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/profiles-overview)
- [OpenAPI](openapi/squarespace-profiles-api-openapi.yml)

### Squarespace Transactions API
The Squarespace Transactions API returns Document resource objects representing collections of financial transactions for orders and donations on a merchant site. It provides detailed payment data and supports multiple payment gateways including Squarespace Payments, Stripe, PayPal, and Square. The API is useful for building financial reporting tools, reconciliation workflows, and accounting integrations. Access to the Transactions API requires a Commerce Basic, Commerce Advanced, or higher Squarespace plan.

**Human URL:** [https://developers.squarespace.com/commerce-apis/transactions-overview](https://developers.squarespace.com/commerce-apis/transactions-overview)


#### Tags:

 - Transactions, Payments, Finance, Commerce

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/transactions-overview)
- [OpenAPI](openapi/squarespace-transactions-api-openapi.yml)

### Squarespace Webhook Subscriptions API
The Squarespace Webhook Subscriptions API allows developers to subscribe to event notifications from a Squarespace site. Supported event topics include order creation, order updates, and extension uninstalls, enabling real-time integrations with external systems. The API supports creating, updating, retrieving, and deleting webhook subscriptions, as well as sending test notifications and rotating subscription secrets. All webhook subscription requests require OAuth token authentication.

**Human URL:** [https://developers.squarespace.com/commerce-apis/webhook-subscriptions-overview](https://developers.squarespace.com/commerce-apis/webhook-subscriptions-overview)


#### Tags:

 - Webhooks, Events, Commerce, Notifications

#### Properties

- [Documentation](https://developers.squarespace.com/commerce-apis/webhook-subscriptions-overview)
- [OpenAPI](openapi/squarespace-webhook-subscriptions-api-openapi.yml)
- [AsyncAPI](asyncapi/squarespace-webhooks-asyncapi.yml)

### Squarespace Developer Platform
The Squarespace Developer Platform provides tools for web developers to access, customize, and build upon the template files underlying Squarespace websites. Using Developer Mode, developers can access the template repository via Git, edit HTML, CSS, JavaScript, and JSON Template markup, and create fully custom Squarespace-hosted templates. The platform includes a local development server for testing changes before pushing them live. It is designed for advanced use cases where standard Squarespace customization options are insufficient, such as bespoke client sites or agency-built templates.

**Human URL:** [https://developers.squarespace.com/](https://developers.squarespace.com/)


#### Tags:

 - Templates, Developer Tools, Custom Code, Website Builder

#### Properties

- [Documentation](https://developers.squarespace.com/)

### Squarespace OAuth
Squarespace OAuth 2.0 enables third-party applications to obtain authorized access to Squarespace merchant sites on behalf of site owners. Developers register their applications in the Squarespace Developer portal, then implement the standard OAuth authorization code flow to request scoped access tokens. These tokens are used to authenticate requests to all Squarespace Commerce APIs. OAuth is required for building Squarespace Extensions and other integrations that access multiple merchant accounts.

**Human URL:** [https://developers.squarespace.com/oauth](https://developers.squarespace.com/oauth)


#### Tags:

 - OAuth, Authentication, Authorization, Security

#### Properties

- [Documentation](https://developers.squarespace.com/oauth)

## Common Properties

- [Portal](https://developers.squarespace.com/)
- [Documentation](https://developers.squarespace.com/commerce-apis/overview)
- [Website](https://www.squarespace.com/)
- [PrivacyPolicy](https://www.squarespace.com/privacy)
- [TermsOfService](https://www.squarespace.com/terms-of-service)
- [Support](https://support.squarespace.com/)
- [Blog](https://www.squarespace.com/blog/)
- [Login](https://account.squarespace.com/)

## Maintainers

**FN:** API Evangelist

**Email:** info@apievangelist.com
