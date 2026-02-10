# Chargebee Webhook Events

## Overview

Chargebee sends webhook notifications for important billing events. Webhooks are asynchronous and may:
- Arrive out of order
- Be delivered multiple times
- Include a delay between the actual event and delivery

**Best practices:**
- Verify webhook signatures
- Implement idempotency using `event.id`
- Return 200 OK quickly (process asynchronously)
- Handle all event types gracefully

## Webhook Payload Structure

```json
{
  "id": "ev_123",
  "occurred_at": 1234567890,
  "source": "admin_console",
  "event_type": "customer_created",
  "webhook_status": "scheduled",
  "content": {
    "customer": {
      "id": "cust_123",
      // ... customer object fields
    }
  }
}
```

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
Sent as the trial period approaches completion (typically 3 days before).

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
Fired when a subscription is cancelled.

**Content**: `subscription` object, `customer` object

### subscription_reactivated
Sent when a cancelled subscription returns to active or trial state.

**Content**: `subscription` object, `customer` object

### subscription_deleted
Triggered when a subscription is permanently deleted.

**Content**: `subscription` object, `customer` object

## Invoice Events

### invoice_generated
Fired when an invoice is created (draft or posted).

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

## Webhook Verification

Verify webhook authenticity using the signature header:

```python
import chargebee

def verify_webhook(payload, signature):
    try:
        chargebee.Webhook.verify_signature(payload, signature)
        return True
    except Exception as e:
        return False
```

The signature is sent in the `X-Chargebee-Signature` header.

## Idempotency

Always check `event.id` to avoid processing duplicate webhooks:

```python
processed_events = set()  # Or use a database

def handle_webhook(event):
    event_id = event['id']

    if event_id in processed_events:
        return  # Already processed

    # Process event
    process_event(event)

    # Mark as processed
    processed_events.add(event_id)
```

## Retry Behavior

Chargebee retries failed webhooks (non-200 responses) with exponential backoff:
- First retry: After 5 minutes
- Subsequent retries: Increasing intervals
- Maximum retries: Continues for up to 3 days

Return 200 OK to acknowledge successful receipt.
