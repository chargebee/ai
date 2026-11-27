# Chargebee API Reference

## Authentication

All API requests use HTTP Basic authentication. The API key is the username and the password is empty, so the header is the Base64 encoding of the key followed by a colon:

```
Authorization: Basic base64("<api_key>:")
```

With curl, pass `-u <api_key>:` (note the trailing colon). Most HTTP clients accept the key and an empty password directly, for example `auth=(api_key, "")` in Python `requests`.

Base URL: `https://[your-site].chargebee.com/api/v2`

### Authentication Security

- Store API keys in server-side environment variables only.
- Never embed API keys in frontend code, mobile binaries, or public repositories.
- Never log full API keys or include them in error messages.
- Rotate keys regularly and revoke compromised credentials immediately.
- Use separate keys for development, staging, and production.

## HTTP Methods

- **GET**: Read-only operations (retrieve, list)
- **POST**: Write operations (create, update, delete)

## Request and Response format

A majority of the API endpoints expect the request to be of type `application/x-www-form-urlencoded`. Nested objects are expected to conform to the commonly used **extended** URL encoding pattern. For example, a JSON request and its equivalent URL encoded `curl` request is shown below:

JSON:

```json
{
  "customer": {
    "first_name": "John",
    "last_name": "Doe",
    "allow_direct_debit": true,
    "bank_account": {
      "account_number": "000222222227",
      "bank_name": "US Bank",
      "account_type": "savings"
    }
  }
}
```

URL Encoded:

```bash
curl  https://{CHARGEBEE_SITE}.chargebee.com/api/v2/customers \
  -X POST  \
  -u {site_api_key}:\
  -d "first_name"="John" \
  -d "last_name"="Doe" \
  -d "allow_direct_debit"="true" \
  -d "bank_account[account_number]"=000222222227 \
  -d "bank_account[routing_number]"=110000000 \
  -d "bank_account[bank_name]"="US Bank" \
  -d "bank_account[account_type]"="savings"
```

All responses are of type `application/json`.

## Core Resources

### Customers

**Create Customer**
```
POST /customers
```
Body parameters:
- `id` (optional): Custom customer identifier
- `first_name`: Customer first name
- `last_name`: Customer last name
- `email`: Contact email
- `phone`: Phone number
- `company`: Company name
- `auto_collection`: on/off (payment automation)
- `billing_address`: Address object

**Retrieve Customer**
```
GET /customers/{customer-id}
```

**Update Customer**
```
POST /customers/{customer-id}
```
Accepts same parameters as create (updates specified fields only)

**List Customers**
```
GET /customers
```
Query parameters:
- `limit`: Results per page (default 10, max 100)
- `offset`: Pagination offset
- `email[is]`: Filter by email
- `created_at[after]`: Filter by creation date

**Delete Customer**
```
POST /customers/{customer-id}/delete
```

### Subscriptions

These are the Product Catalog 2.0 operations. Do not use `POST /subscriptions`, `POST /subscriptions/{subscription-id}` or `POST /subscriptions/{subscription-id}/cancel` with `plan_id` and `addons`; those are Product Catalog 1.0 operations.

**Create Subscription for a Customer**
```
POST /customers/{customer-id}/subscription_for_items
```
Body parameters:
- `subscription_items[item_price_id][0]`: The plan item price, followed by any addon or charge item prices at indexes 1, 2, …
- `subscription_items[quantity][0]`: Quantity, for per-unit, tiered, volume and stairstep pricing
- `billing_cycles`: Number of billing cycles
- `trial_end`: Trial end timestamp
- `auto_collection`: on/off

**Retrieve Subscription**
```
GET /subscriptions/{subscription-id}
```

**Update Subscription Items**
```
POST /subscriptions/{subscription-id}/update_for_items
```
Body parameters:
- `subscription_items[item_price_id][0]`, `subscription_items[quantity][0]`: The items to add or change
- `replace_items_list`: true to replace the whole item list instead of merging
- `change_option`: immediately/end_of_term/specific_date. `specific_date` requires `changes_scheduled_at`. To schedule a future change, use the ramps API (`POST /subscriptions/{subscription-id}/create_ramp`); a future `changes_scheduled_at` is deprecated for scheduling.
- `prorate`: true/false
- `invoice_immediately`: true/false

Preview the cost of a change first with `POST /estimates/update_subscription_for_items`.

**Cancel Subscription**
```
POST /subscriptions/{subscription-id}/cancel_for_items
```
Parameters:
- `cancel_option`: immediately/end_of_term/specific_date/end_of_billing_term. Use this instead of the older `end_of_term` boolean. With `end_of_term` the subscription becomes `non_renewing` until the term ends.
- `cancel_at`: The cancellation date, required with `specific_date`
- `contract_term_cancel_option`: Use instead of `cancel_option` when the subscription has a contract term

**Reactivate Subscription**
```
POST /subscriptions/{subscription-id}/reactivate
```

**List Subscriptions**
```
GET /subscriptions
```
Query parameters:
- `customer_id[is]`: Filter by customer
- `status[is]`: future/in_trial/active/non_renewing/paused/cancelled/transferred
- `limit`, `offset`: Pagination

### Invoices

**Create Invoice for One-off Charges**
```
POST /invoices/create_for_charge_items_and_charges
```
Body parameters:
- `customer_id`: Existing customer ID
- `item_prices[item_price_id][0]`: Charge item price to bill
- `charges[amount][0]`, `charges[description][0]`: Ad hoc charge, in the smallest currency unit

**Retrieve Invoice**
```
GET /invoices/{invoice-id}
```

**List Invoices**
```
GET /invoices
```
Query parameters:
- `customer_id[is]`: Filter by customer
- `status[is]`: paid/posted/payment_due/not_paid/voided/pending
- `date[after]`, `date[before]`: Date filters

**Void Invoice**
```
POST /invoices/{invoice-id}/void
```

**Collect Payment**
```
POST /invoices/{invoice-id}/collect_payment
```

### Payment Sources

**Create Payment Source from a Chargebee.js Token**
```
POST /payment_sources/create_using_token
```
Parameters:
- `customer_id`: Existing customer ID
- `token_id`: Token created in the browser by Chargebee.js

This endpoint cannot store a card after a successful 3DS flow. For those cards, store the card with `POST /payment_sources/create_using_payment_intent`.

Collect card and bank details in the browser with Chargebee.js or a hosted page (`POST /hosted_pages/manage_payment_sources`). Do not send raw card numbers through your server unless your integration is PCI DSS compliant for handling card data.

**Retrieve Payment Source**
```
GET /payment_sources/{payment-source-id}
```

**Delete Payment Source**
```
POST /payment_sources/{payment-source-id}/delete
```

### Product Catalog

Product Catalog 2.0 models what you sell as item families, items and item prices. A plan, an addon and a one-off charge are each an item of type `plan`, `addon` or `charge`, and each item has one item price per currency and billing period. If price variants are enabled, an item can have several item prices for the same currency and billing period, each with a distinct `price_variant_id`. The `/plans` and `/addons` endpoints belong to Product Catalog 1.0; do not use them for new integrations.

**Create Item Family**
```
POST /item_families
```
Body parameters:
- `id`: Item family identifier
- `name`: Display name

**Create Item**
```
POST /items
```
Body parameters:
- `id`: Item identifier
- `name`: Display name
- `type`: plan/addon/charge
- `item_family_id`: The item family it belongs to

**Create Item Price**
```
POST /item_prices
```
Body parameters:
- `id`: Item price identifier, for example `pro-USD-monthly`
- `item_id`: The item it prices
- `name`: Display name
- `pricing_model`: flat_fee/per_unit/tiered/volume/stairstep
- `price`: Price in the smallest currency unit (for example cents), for flat_fee and per_unit
- `currency_code`: For example `USD`
- `period`: Number of period units in a billing cycle, for example `1`
- `period_unit`: day/week/month/year

**Retrieve and List**
```
GET /items/{item-id}
GET /items
GET /item_prices/{item-price-id}
GET /item_prices?item_id[is]={item-id}
```

### Transactions

**List Transactions**
```
GET /transactions
```
Query parameters:
- `customer_id[is]`: Filter by customer
- `subscription_id[is]`: Filter by subscription
- `date[after]`, `date[before]`: Date range

**Retrieve Transaction**
```
GET /transactions/{transaction-id}
```

## Common Response Structure

Successful responses contain the requested resource(s):

```json
{
  "customer": {
    "id": "cust_123",
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    // ... more fields
  }
}
```

List responses include pagination:

```json
{
  "list": [
    { "customer": { /* ... */ } },
    { "customer": { /* ... */ } }
  ],
  "next_offset": "[encoded-offset]"
}
```

## Error Responses

Errors return appropriate HTTP status codes with error details:

```json
{
  "message": "Error message",
  "type": "invalid_request",
  "api_error_code": "param_wrong_value",
  "param": "subscription_items[item_price_id][0]"
}
```

Error attributes:
- `message`: For developers. Do not show it to customers.
- `type` (optional): `payment`, `invalid_request` or `operation_failed`. SDKs raise a matching exception class.
- `api_error_code`: The specific code to branch on, for example `resource_not_found`, `payment_processing_failed` or `param_wrong_value`.
- `param` (optional): The parameter that caused the error.
- `error_cause_id` (optional): A gateway error code, listed in **references/errors.md**.

Full list of error codes and recommended handling: https://apidocs.chargebee.com/docs/api/error-handling.md

## Pagination

Use `limit` and `offset` for pagination:

```
GET /customers?limit=10&offset=[encoded-offset]
```

The response includes `next_offset` for fetching the next page.

## Filters

Most list endpoints support filtering:

```
GET /subscriptions?status[is]=active&customer_id[is]=cust_123
```

Filter operators by attribute type:

| Attribute type | Operators |
| --- | --- |
| String | `[is]`, `[is_not]`, `[starts_with]`, `[in]`, `[not_in]`, `[is_present]` |
| Enumerated string | `[is]`, `[is_not]`, `[in]`, `[not_in]`, `[is_present]` |
| Number | `[is]`, `[is_not]`, `[gt]`, `[gte]`, `[lt]`, `[lte]`, `[between]`, `[is_present]` |
| Timestamp or date | `[on]`, `[before]`, `[after]`, `[between]`, `[is_present]` |
| Boolean | `[is]`, `[is_present]` |

`[in]` and `[not_in]` take a JSON array, for example `status[in]=["active","in_trial"]`. `[between]` takes two values, for example `created_at[between]=[1700000000,1702592000]`. `[is_present]` takes `true` or `false`.

Not every attribute supports every operator; the list operation page for each resource shows which ones it accepts. Details: https://apidocs.chargebee.com/docs/api/list-ops.md

## Idempotency

Make POST requests safe to retry by sending a unique `chargebee-idempotency-key` header. For 30 minutes, a request with the same key and parameters is treated as a replay of the original and returns the original result. Replayed responses carry the `chargebee-idempotency-replayed` header. Details: https://apidocs.chargebee.com/docs/api/idempotency.md

## Rate Limiting

Chargebee limits API requests per site per minute (150 on test sites; on live sites it depends on the plan) and also limits concurrent requests. Exceeding a limit returns HTTP `429` with an `api_error_code` such as `api_request_limit_exceeded` or `lock_timeout` (concurrent updates to the same resource). If the response has a `Retry-After` header, wait that many seconds before retrying; otherwise back off exponentially. Details: https://apidocs.chargebee.com/docs/api/error-handling.md#api_rate_limits
