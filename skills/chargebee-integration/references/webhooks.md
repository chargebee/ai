# Chargebee Webhook Events

## Overview

Chargebee sends webhook notifications for important billing events. Webhooks are asynchronous and may:
- Arrive out of order
- Be delivered multiple times
- Include a delay between the actual event and delivery

**Best practices:**
- Validate webhook requests with Basic Auth
- Implement idempotency using `event.id`
- Ignore stale updates using the resource's `resource_version`
- Return a `2XX` status quickly and process asynchronously
- Handle all event types gracefully, including types you do not use

Each webhook is an HTTP POST with content type `application/json`. Reference: https://apidocs.chargebee.com/docs/api/events.md

## Webhook Payload Structure

```json
{
  "id": "ev_123",
  "occurred_at": 1702645601,
  "source": "admin_console",
  "object": "event",
  "api_version": "v2",
  "event_type": "customer_created",
  "content": {
    "customer": {
      "id": "cust_123",
      "resource_version": 1702645601793
      // ... customer object fields
    }
  }
}
```

Check that `api_version` matches the API version of the client library your webhook server uses.

## Customer Events

### customer_created
Triggered when a new customer is created, either independently or during subscription creation.

**Content**: `customer` object

### customer_changed
Fired when customer information is modified.

**Content**: `customer` object

### customer_deleted
Sent when a customer is deleted from the system.

**Content**: `customer` object (with deleted state)

### customer_moved_out
Triggered when a customer is copied to another Chargebee site.

**Content**: `customer` object

### customer_moved_in
Fired when a customer is copied from another Chargebee site.

**Content**: `customer` object

### promotional_credits_added
Sent when promotional credits are added to a customer account.

**Content**: `customer` object, `promotional_credits` object

### promotional_credits_deducted
Triggered when promotional credits are removed from an account.

**Content**: `customer` object, `promotional_credits` object

## Subscription Events

### subscription_created
Sent when a new subscription is established.

**Content**: `subscription` object, `customer` object

### subscription_created_with_backdating
Fired when subscription creation includes backdated changes.

**Content**: `subscription` object, `customer` object

### subscription_started
Triggered when a future subscription begins at the scheduled start date.

**Content**: `subscription` object, `customer` object

### subscription_trial_end_reminder
Sent 6 days before the trial period ends.

**Content**: `subscription` object, `customer` object

### subscription_activated
Fired when a subscription transitions from trial to active state.

**Content**: `subscription` object, `customer` object

### subscription_changed
Activated when subscription items (plans, addons, quantities) are modified.

**Content**: `subscription` object, `customer` object

### subscription_trial_extended
Sent when the trial period is extended.

**Content**: `subscription` object, `customer` object

### subscription_renewed
Triggered when a subscription renews for a new term.

**Content**: `subscription` object, `customer` object, `invoice` object

### subscription_paused
Sent when a subscription is paused.

**Content**: `subscription` object, `customer` object

### subscription_resumed
Triggered when a paused subscription resumes.

**Content**: `subscription` object, `customer` object

### subscription_cancelled
Fired when a subscription is cancelled. If it was cancelled for non-payment or because no card was present, `subscription.cancel_reason` says so.

**Content**: `subscription` object, `customer` object

### subscription_reactivated
Sent when a cancelled subscription returns to active or trial state.

**Content**: `subscription` object, `customer` object

### subscription_deleted
Triggered when a subscription is permanently deleted.

**Content**: `subscription` object, `customer` object

## Invoice Events

### invoice_generated
Fired when a new invoice is generated. For metered billing, fired when a pending invoice is closed.

**Content**: `invoice` object, `customer` object

### invoice_updated
Sent when invoice details are modified.

**Content**: `invoice` object, `customer` object

### invoice_deleted
Triggered when an invoice is deleted.

**Content**: `invoice` object, `customer` object

## Payment Events

### payment_succeeded
Sent when a payment is successfully processed.

**Content**: `transaction` object, `customer` object, `invoice` object

### payment_failed
Triggered when a payment attempt fails.

**Content**: `transaction` object, `customer` object, `invoice` object

### payment_refunded
Fired when a refund is issued.

**Content**: `transaction` object, `customer` object, `invoice` object

### payment_source_added
Sent when a payment method is added to a customer.

**Content**: `payment_source` object, `customer` object

### payment_source_updated
Triggered when payment source details are modified.

**Content**: `payment_source` object, `customer` object

### payment_source_deleted
Fired when a payment method is removed.

**Content**: `payment_source` object, `customer` object

## Coupon/Offer Events

### coupon_created
Sent when a new coupon is created.

**Content**: `coupon` object

### coupon_updated
Triggered when coupon details are modified.

**Content**: `coupon` object

### coupon_deleted
Fired when a coupon is deleted.

**Content**: `coupon` object

### coupon_set_created
Sent when a coupon set is created.

**Content**: `coupon_set` object

### coupon_set_updated
Triggered when a coupon set is modified.

**Content**: `coupon_set` object

### coupon_set_deleted
Fired when a coupon set is deleted.

**Content**: `coupon_set` object

### coupon_codes_added
Sent when individual coupon codes are added.

**Content**: `coupon_code` objects

### coupon_codes_updated
Triggered when coupon codes are modified.

**Content**: `coupon_code` objects

### coupon_codes_deleted
Fired when coupon codes are removed.

**Content**: `coupon_code` objects

## Billing Events

### mrr_updated
Sent when Monthly Recurring Revenue (MRR) or committed MRR changes.

**Content**: `mrr` object, `subscription` object, `customer` object

## Webhook Authentication

Validate webhook authenticity using Basic Auth credentials configured for your webhook endpoint.

```python
import os
import secrets

WEBHOOK_USERNAME = os.getenv("CHARGEBEE_WEBHOOK_USERNAME")
WEBHOOK_PASSWORD = os.getenv("CHARGEBEE_WEBHOOK_PASSWORD")

def is_valid_webhook_auth(auth):
    if not auth or not WEBHOOK_USERNAME or not WEBHOOK_PASSWORD:
        return False
    username_ok = secrets.compare_digest(auth.username or "", WEBHOOK_USERNAME or "")
    password_ok = secrets.compare_digest(auth.password or "", WEBHOOK_PASSWORD or "")
    return username_ok and password_ok
```

Reject requests with invalid or missing credentials before parsing and processing payloads.

To turn on Basic Auth, enable **Protect webhook URL with basic authentication** in the webhook settings and set a username and password. To confirm an event is genuine, you can also fetch it again with `GET /events/{event-id}` and process the fetched copy. Chargebee sends webhooks from a fixed set of IP addresses: https://apidocs.chargebee.com/docs/api/webhooks.md

## Idempotency

Chargebee can deliver the same event more than once. Deduplicate on `event.id`:

- Save each event to a persistent inbox, such as a database table with a unique key on `event.id`, in a single write. Then return `2XX`. A duplicate-key error means the event was already received.
- Process inbox rows in a background worker. If processing fails, retry from the inbox: Chargebee retries only deliveries that did not get a `2XX`.
- Make side effects such as emails or provisioning safe to repeat, for example by keying them on `event.id`, because a worker can fail after the effect and run again.
- Keep IDs for at least 3 days and 7 hours, when the last retry arrives.

```python
def receive(event):
    try:
        save_to_inbox(event["id"], event)  # one write; unique key on event id
    except DuplicateKeyError:  # your driver's unique-key violation error
        pass  # already received
    # return 2XX; a background worker processes inbox rows
```

## Out-of-order Delivery

Events can arrive out of order. Most resources carry `resource_version`, a millisecond timestamp updated on each change; some, such as `impacted_items`, do not.

- Update your stored copy of a resource only if the incoming `resource_version` is newer. Make the check and the write one atomic operation, such as a conditional update, so concurrent workers cannot overwrite a newer version with an older one.
- Decide access from the stored subscription state, or by retrieving the subscription from Chargebee, not from the payload of the event being processed. Process events for the same subscription one at a time, for example with a per-subscription lock or queue partition, so two workers cannot act on different versions.
- Work that does not change access, such as recording a renewal, still runs for each new event ID, even when its resource snapshot is older.

```python
def apply_if_newer(resource):
    # A single conditional write that only matches when the stored
    # resource_version is older than resource["resource_version"].
    save_if_newer(resource["id"], resource, resource["resource_version"])
```

## Retry Behavior

A webhook succeeds only when your endpoint returns a `2XX` status within the timeout. Otherwise Chargebee retries it up to 7 times:

| Retry | When |
| --- | --- |
| 1 | 2 minutes after the failure |
| 2 | 6 minutes after the previous retry |
| 3 | 30 minutes after the previous retry |
| 4 | 1 hour after the previous retry |
| 5 | 5 hours after the previous retry |
| 6 | 1 day after the previous retry |
| 7 | 2 days after the previous retry |

Timeouts:

| Timeout | Test site | Live site |
| --- | --- | --- |
| Connection | 10 seconds | 20 seconds |
| Read | 10 seconds | 20 seconds |
| Total webhook execution | 20 seconds | 60 seconds |

Save the event, return a `2XX` status, and process the event afterwards, for example from a queue. A handler that does the processing before it responds can exceed these timeouts, and Chargebee then retries the event. Source: https://www.chargebee.com/docs/billing/2.0/site-configuration/webhook_settings.md
