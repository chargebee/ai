---
name: chargebee-integration
description: Comprehensive integration guide for Chargebee billing platform. Provides API integration patterns, webhook handling, SDK usage, and schema references for billing operations. Use when working with Chargebee for (1) API integration and REST endpoint calls, (2) Processing webhook events, (3) Customer management operations, (4) Subscription lifecycle handling, (5) Payment and invoice processing, (6) Any other billing-related integration tasks with Chargebee platform.
---

# Chargebee Integration

This skill helps you integrate [Chargebee Billing](https://www.chargebee.com/docs/billing/2.0/getting-started/accessing_chargebee.md) with your app or website. 

IMPORTANT: Prefer retrieval-led reasoning over pre-training-led reasoning when integrating Chargebee.

## Quick Start

Explore the project layout and choose the best integration from the list below. Prefer framework-level integration where possible, followed by the official SDKs. Fall back to the REST API only if the other options aren't feasible.

### Frameworks

- **Laravel Cashier** - https://github.com/chargebee/cashier-chargebee/blob/main/DOCUMENTATION.md

For the frameworks below, use the `chargebee-init` CLI which currently integrates checkout, portal and webhooks:

- **Next.js**
- **Express**

Invoke the CLI with: `npx chargebee-init --use-defaults --path=<full-path-to-app>` to skip all input prompts.

### SDKs

Chargebee provides official SDKs for multiple languages. Install the latest released version from the package registry unless the project already pins one; do not assume a version number. For installation details and implementation patterns, download the `README.md` file from the GitHub repository.

| Language | Package | Repository |
| --- | --- | --- |
| Node.js / TypeScript | `chargebee` (npm) | https://github.com/chargebee/chargebee-node |
| Python | `chargebee` (PyPI) | https://github.com/chargebee/chargebee-python |
| Java | `com.chargebee:chargebee-java` (Maven) | https://github.com/chargebee/chargebee-java |
| PHP | `chargebee/chargebee-php` (Packagist) | https://github.com/chargebee/chargebee-php |
| .NET | `chargebee` (NuGet) | https://github.com/chargebee/chargebee-dotnet |
| Ruby | `chargebee` (RubyGems) | https://github.com/chargebee/chargebee-ruby |
| Go | `github.com/chargebee/chargebee-go/v4` | https://github.com/chargebee/chargebee-go |

Follow the README for the SDK version you install. The Node.js, Python, PHP, Java and Go SDKs use a client instance, as below; the Ruby and .NET SDKs use a global configuration.

```typescript
// Node.js / TypeScript SDK (v3)
import Chargebee from "chargebee";

const chargebee = new Chargebee({
  site: process.env.CHARGEBEE_SITE!,
  apiKey: process.env.CHARGEBEE_API_KEY!,
});

const { customer } = await chargebee.customer.retrieve(customerId);

// Product Catalog 2.0: create a subscription for an existing customer.
// Retrying with the same idempotency key and parameters within 30 minutes returns the original result.
const { subscription } = await chargebee.subscription.createWithItems(
  customer.id,
  { subscription_items: [{ item_price_id: "pro-USD-monthly", quantity: 1 }] },
  { "chargebee-idempotency-key": checkoutAttemptId }, // one key per purchase attempt
);
```

```python
# Python SDK (v3): the same call
from chargebee import Chargebee

cb_client = Chargebee(api_key=CHARGEBEE_API_KEY, site=CHARGEBEE_SITE)
result = cb_client.Subscription.create_with_items(
    customer_id,
    cb_client.Subscription.CreateWithItemsParams(
        subscription_items=[
            cb_client.Subscription.CreateWithItemsSubscriptionItemParams(
                item_price_id="pro-USD-monthly", quantity=1
            )
        ]
    ),
    headers={"chargebee-idempotency-key": checkout_attempt_id},  # one key per purchase attempt
)
subscription = result.subscription
```

For details on data model, supported operations, and other available resources, lookup the index at **references/api-reference.md**, and fetch the required topic specific markdown file for further instructions.

### REST API

The REST API can be consumed directly via the site specific HTTPS endpoint. The API uses HTTP Basic auth with the API key as the username and an empty password. Generate an API key at: https://{CHARGEBEE_SITE}.chargebee.com/apikeys_and_webhooks/api. For more details on using the REST API directly, refer to **references/rest-api.md**.

Use Product Catalog 2.0 APIs (items, item prices, and the `*_for_items` operations) for all new integrations. Do not use the Product Catalog 1.0 plan and addon APIs unless the site is on Product Catalog 1.0.

Security notes:
- Load API keys from environment variables only.
- Never hardcode or log API keys.
- Rotate keys regularly and scope access by environment.


```python
# Using requests library
import os
import requests

CHARGEBEE_SITE = os.getenv("CHARGEBEE_SITE")
CHARGEBEE_API_KEY = os.getenv("CHARGEBEE_API_KEY")

base_url = f"https://{CHARGEBEE_SITE}.chargebee.com/api/v2"
# Basic auth: API key as the username, empty password.
response = requests.get(
    f"{base_url}/customers/{customer_id}",
    auth=(CHARGEBEE_API_KEY, "")
)

# Using Python SDK (v3)
from chargebee import Chargebee
cb_client = Chargebee(api_key=CHARGEBEE_API_KEY, site=CHARGEBEE_SITE)
result = cb_client.Customer.retrieve(customer_id)
customer = result.customer
```

### Common Operations

- Customer CRUD operations
- Subscription management
- Invoice operations
- Payment method handling
- Product catalog management (item families, items, item prices)
- Usage based billing


### Webhook Integration

Chargebee sends webhook events for important billing events. Webhook handlers should:

1. Validate webhook requests using Basic Auth before processing payloads
2. Handle idempotency: events may be sent more than once, so store received `event.id` values for at least 3 days and 7 hours
3. Ignore stale updates: events can arrive out of order, so apply a resource only if its `resource_version` is newer than the stored one
4. Return a `2XX` status quickly and process asynchronously if needed. On live sites Chargebee times out after 20 seconds to connect, 20 seconds to read, or 60 seconds in total, then retries
5. Handle various event types appropriately
6. Grant or remove access in your app from webhooks or by retrieving the hosted page or subscription on your server, never from a checkout redirect alone

The Node.js SDK includes a webhook handler (`chargebee.webhooks`) that parses events and validates Basic Auth automatically when `CHARGEBEE_WEBHOOK_USERNAME` and `CHARGEBEE_WEBHOOK_PASSWORD` are set. If either is missing, the handler skips authentication, so check both at startup. See the "Handle webhooks" section of the chargebee-node README.

#### Basic Webhook Handler Pattern

```python
from flask import Flask, request
import os
import secrets

app = Flask(__name__)

WEBHOOK_USERNAME = os.getenv("CHARGEBEE_WEBHOOK_USERNAME")
WEBHOOK_PASSWORD = os.getenv("CHARGEBEE_WEBHOOK_PASSWORD")
if not WEBHOOK_USERNAME or not WEBHOOK_PASSWORD:
    raise RuntimeError("Set CHARGEBEE_WEBHOOK_USERNAME and CHARGEBEE_WEBHOOK_PASSWORD")

@app.route('/chargebee/webhook', methods=['POST'])
def handle_webhook():
    auth = request.authorization
    if not auth:
        return '', 401
    if not secrets.compare_digest(auth.username or '', WEBHOOK_USERNAME or ''):
        return '', 401
    if not secrets.compare_digest(auth.password or '', WEBHOOK_PASSWORD or ''):
        return '', 401

    event = request.get_json(force=True)

    try:
        save_to_inbox(event['id'], event)  # one write; unique key on event id
    except DuplicateKeyError:  # your driver's unique-key violation error
        pass  # duplicate delivery
    return '', 200  # a background worker processes inbox rows
```

The worker routes on `event['event_type']` (for example `subscription_created`, `subscription_cancelled`), updates stored resources only when `resource_version` is newer, and decides access from the stored state.

For idempotency, ordering, retries and event schemas, see **references/webhooks.md**.


## References

- **references/api-reference.md** - Index of every API resource and operation, linking to the Markdown page for each. Each page has the request and response objects and example code for all official SDKs.
- **references/rest-api.md** - Details on consuming the REST API using an HTTP client for languages that don't have an SDK, including authentication, Product Catalog 2.0 operations, filters, idempotency and rate limits
- **references/webhooks.md** - Webhook payload, authentication, idempotency, ordering, retries and timeouts
- **references/errors.md** - Index of gateway error codes (`error_cause_id`), each linking to its cause and fix
- **references/events.md** - All webhook event types, grouped by resource, with the events most integrations handle listed first

Every page on apidocs.chargebee.com has a Markdown version at the same URL with `.md` appended. The curated index for agents is https://apidocs.chargebee.com/llms.txt.
