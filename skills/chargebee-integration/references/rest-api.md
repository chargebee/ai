# Chargebee API Reference

## Authentication

All API requests require Basic Authentication with your API key:

```
Authorization: Basic <api_key>
```

Base URL: `https://[your-site].chargebee.com/api/v2`

## HTTP Methods

- **GET**: Read-only operations (retrieve, list)
- **POST**: Write operations (create, update, delete)

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

**Create Subscription**
```
POST /subscriptions
```
Body parameters:
- `plan_id`: The plan identifier
- `customer_id`: Existing customer ID
- `billing_cycles`: Number of billing cycles
- `trial_end`: Trial end timestamp
- `auto_collection`: on/off
- `addons`: Array of addon objects

**Retrieve Subscription**
```
GET /subscriptions/{subscription-id}
```

**Update Subscription**
```
POST /subscriptions/{subscription-id}
```

**Cancel Subscription**
```
POST /subscriptions/{subscription-id}/cancel
```
Parameters:
- `end_of_term`: true/false (cancel immediately or at term end)

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
- `status[is]`: active/cancelled/non_renewing/in_trial
- `limit`, `offset`: Pagination

### Invoices

**Create Invoice**
```
POST /invoices
```

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
- `status[is]`: paid/posted/payment_due/not_paid
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

**Create Payment Source**
```
POST /customers/{customer-id}/payment_sources
```
Parameters:
- `type`: card/bank_account/paypal
- `gateway_account_id`: Payment gateway identifier
- Card/bank details as needed

**Retrieve Payment Source**
```
GET /payment_sources/{payment-source-id}
```

**Delete Payment Source**
```
POST /payment_sources/{payment-source-id}/delete
```

### Plans

**Create Plan**
```
POST /plans
```
Body parameters:
- `id`: Plan identifier
- `name`: Plan display name
- `price`: Plan price in cents
- `period`: Billing period (day/week/month/year)
- `period_unit`: Number of periods

**Retrieve Plan**
```
GET /plans/{plan-id}
```

**List Plans**
```
GET /plans
```

**Update Plan**
```
POST /plans/{plan-id}
```

### Addons

**Create Addon**
```
POST /addons
```

**Retrieve Addon**
```
GET /addons/{addon-id}
```

**List Addons**
```
GET /addons
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
  "api_error_code": "resource_not_found"
}
```

Common error codes:
- `payment_processing_failed`
- `resource_not_found`
- `invalid_request`
- `operation_failed`

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

Available filter operators:
- `[is]`: Exact match
- `[is_not]`: Not equal
- `[in]`: In array (comma-separated)
- `[after]`, `[before]`: Date comparisons
- `[starts_with]`: String prefix matching

## Rate Limiting

Chargebee enforces rate limits per site. Respect `Retry-After` headers in 429 responses.
