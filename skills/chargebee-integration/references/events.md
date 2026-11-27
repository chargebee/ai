# Webhook Events

Every event type Chargebee sends, grouped by resource. Each link opens the event's payload reference. The full index is at https://apidocs.chargebee.com/docs/api/events.md.

## Events most integrations handle

A subscription integration that grants access in the app usually handles these:

- `subscription_created`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_created.md
- `subscription_started`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_started.md
- `subscription_activated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_activated.md
- `subscription_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_changed.md
- `subscription_renewed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_renewed.md
- `subscription_cancellation_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_cancellation_scheduled.md
- `subscription_scheduled_cancellation_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_scheduled_cancellation_removed.md
- `subscription_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_cancelled.md
- `subscription_reactivated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_reactivated.md
- `subscription_paused`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_paused.md
- `subscription_resumed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_resumed.md
- `subscription_trial_end_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_trial_end_reminder.md
- `subscription_changes_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_changes_scheduled.md
- `payment_succeeded`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_succeeded.md
- `payment_failed`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_failed.md
- `payment_refunded`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_refunded.md
- `invoice_generated`: https://apidocs.chargebee.com/docs/api/events/webhook/invoice_generated.md
- `invoice_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/invoice_updated.md
- `customer_created`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_created.md
- `customer_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_changed.md
- `payment_source_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_updated.md
- `card_expiry_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/card_expiry_reminder.md
- `subscription_entitlements_created`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_entitlements_created.md
- `subscription_entitlements_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_entitlements_updated.md

## All events

### attached_item

- `attached_item_created`: https://apidocs.chargebee.com/docs/api/events/webhook/attached_item_created.md
- `attached_item_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/attached_item_deleted.md
- `attached_item_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/attached_item_updated.md

### authorization

- `authorization_succeeded`: https://apidocs.chargebee.com/docs/api/events/webhook/authorization_succeeded.md
- `authorization_voided`: https://apidocs.chargebee.com/docs/api/events/webhook/authorization_voided.md

### business_entity

- `business_entity_created`: https://apidocs.chargebee.com/docs/api/events/webhook/business_entity_created.md
- `business_entity_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/business_entity_deleted.md
- `business_entity_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_entity_updated.md

### business_rule

- `business_rule_activated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_rule_activated.md
- `business_rule_created`: https://apidocs.chargebee.com/docs/api/events/webhook/business_rule_created.md
- `business_rule_deactivated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_rule_deactivated.md
- `business_rule_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/business_rule_deleted.md
- `business_rule_released`: https://apidocs.chargebee.com/docs/api/events/webhook/business_rule_released.md
- `business_rule_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_rule_updated.md

### business_ruleset

- `business_ruleset_activated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_ruleset_activated.md
- `business_ruleset_created`: https://apidocs.chargebee.com/docs/api/events/webhook/business_ruleset_created.md
- `business_ruleset_deactivated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_ruleset_deactivated.md
- `business_ruleset_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/business_ruleset_deleted.md
- `business_ruleset_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/business_ruleset_updated.md

### card

- `card_added`: https://apidocs.chargebee.com/docs/api/events/webhook/card_added.md
- `card_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/card_deleted.md
- `card_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/card_expired.md
- `card_expiry_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/card_expiry_reminder.md
- `card_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/card_updated.md

### chargeback

- `chargeback_initiated`: https://apidocs.chargebee.com/docs/api/events/webhook/chargeback_initiated.md
- `chargeback_lost`: https://apidocs.chargebee.com/docs/api/events/webhook/chargeback_lost.md
- `chargeback_won`: https://apidocs.chargebee.com/docs/api/events/webhook/chargeback_won.md

### collections

- `collections_dispute_created`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_dispute_created.md
- `collections_dispute_resolved`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_dispute_resolved.md
- `collections_dispute_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_dispute_updated.md
- `collections_dispute_withdrawn`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_dispute_withdrawn.md
- `collections_payment_promise_broken`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_payment_promise_broken.md
- `collections_payment_promise_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_payment_promise_cancelled.md
- `collections_payment_promise_created`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_payment_promise_created.md
- `collections_payment_promise_fulfilled`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_payment_promise_fulfilled.md
- `collections_payment_promise_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_payment_promise_updated.md
- `collections_reminder_sequence_completed`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_reminder_sequence_completed.md
- `collections_reminder_sequence_created`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_reminder_sequence_created.md
- `collections_reminder_sequence_paused`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_reminder_sequence_paused.md
- `collections_reminder_sequence_resumed`: https://apidocs.chargebee.com/docs/api/events/webhook/collections_reminder_sequence_resumed.md

### contract_term

- `contract_term_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/contract_term_cancelled.md
- `contract_term_completed`: https://apidocs.chargebee.com/docs/api/events/webhook/contract_term_completed.md
- `contract_term_created`: https://apidocs.chargebee.com/docs/api/events/webhook/contract_term_created.md
- `contract_term_renewed`: https://apidocs.chargebee.com/docs/api/events/webhook/contract_term_renewed.md
- `contract_term_terminated`: https://apidocs.chargebee.com/docs/api/events/webhook/contract_term_terminated.md

### coupon

- `coupon_codes_added`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_codes_added.md
- `coupon_codes_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_codes_deleted.md
- `coupon_codes_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_codes_updated.md
- `coupon_created`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_created.md
- `coupon_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_deleted.md
- `coupon_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_updated.md

### coupon_set

- `coupon_set_created`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_set_created.md
- `coupon_set_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_set_deleted.md
- `coupon_set_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/coupon_set_updated.md

### credit_note

- `credit_note_created`: https://apidocs.chargebee.com/docs/api/events/webhook/credit_note_created.md
- `credit_note_created_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/credit_note_created_with_backdating.md
- `credit_note_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/credit_note_deleted.md
- `credit_note_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/credit_note_updated.md

### customer

- `customer_business_entity_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_business_entity_changed.md
- `customer_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_changed.md
- `customer_created`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_created.md
- `customer_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_deleted.md
- `customer_entitlements_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_entitlements_updated.md
- `customer_moved_in`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_moved_in.md
- `customer_moved_out`: https://apidocs.chargebee.com/docs/api/events/webhook/customer_moved_out.md

### differential_price

- `differential_price_created`: https://apidocs.chargebee.com/docs/api/events/webhook/differential_price_created.md
- `differential_price_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/differential_price_deleted.md
- `differential_price_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/differential_price_updated.md

### einvoice

- `einvoice_created`: https://apidocs.chargebee.com/docs/api/events/webhook/einvoice_created.md
- `einvoice_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/einvoice_updated.md

### entitlement_overrides

- `entitlement_overrides_auto_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/entitlement_overrides_auto_removed.md
- `entitlement_overrides_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/entitlement_overrides_removed.md
- `entitlement_overrides_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/entitlement_overrides_updated.md

### feature

- `feature_activated`: https://apidocs.chargebee.com/docs/api/events/webhook/feature_activated.md
- `feature_archived`: https://apidocs.chargebee.com/docs/api/events/webhook/feature_archived.md
- `feature_created`: https://apidocs.chargebee.com/docs/api/events/webhook/feature_created.md
- `feature_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/feature_deleted.md
- `feature_reactivated`: https://apidocs.chargebee.com/docs/api/events/webhook/feature_reactivated.md
- `feature_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/feature_updated.md

### gift

- `gift_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/gift_cancelled.md
- `gift_claimed`: https://apidocs.chargebee.com/docs/api/events/webhook/gift_claimed.md
- `gift_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/gift_expired.md
- `gift_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/gift_scheduled.md
- `gift_unclaimed`: https://apidocs.chargebee.com/docs/api/events/webhook/gift_unclaimed.md
- `gift_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/gift_updated.md

### grant_blocks

- `grant_blocks_created`: https://apidocs.chargebee.com/docs/api/events/webhook/grant_blocks_created.md
- `grant_blocks_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/grant_blocks_updated.md

### hierarchy

- `hierarchy_created`: https://apidocs.chargebee.com/docs/api/events/webhook/hierarchy_created.md
- `hierarchy_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/hierarchy_deleted.md

### invoice

- `invoice_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/invoice_deleted.md
- `invoice_generated`: https://apidocs.chargebee.com/docs/api/events/webhook/invoice_generated.md
- `invoice_generated_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/invoice_generated_with_backdating.md
- `invoice_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/invoice_updated.md

### item

- `item_created`: https://apidocs.chargebee.com/docs/api/events/webhook/item_created.md
- `item_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/item_deleted.md
- `item_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/item_updated.md

### item_entitlements

- `item_entitlements_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/item_entitlements_removed.md
- `item_entitlements_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/item_entitlements_updated.md

### item_family

- `item_family_created`: https://apidocs.chargebee.com/docs/api/events/webhook/item_family_created.md
- `item_family_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/item_family_deleted.md
- `item_family_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/item_family_updated.md

### item_price

- `item_price_created`: https://apidocs.chargebee.com/docs/api/events/webhook/item_price_created.md
- `item_price_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/item_price_deleted.md
- `item_price_entitlements_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/item_price_entitlements_removed.md
- `item_price_entitlements_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/item_price_entitlements_updated.md
- `item_price_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/item_price_updated.md

### ledger

- `ledger_account_balance_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/ledger_account_balance_updated.md
- `ledger_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/ledger_updated.md

### mrr

- `mrr_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/mrr_updated.md

### omnichannel_one_time_order

- `omnichannel_one_time_order_created`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_one_time_order_created.md
- `omnichannel_one_time_order_item_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_one_time_order_item_cancelled.md

### omnichannel_subscription

- `omnichannel_subscription_created`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_created.md
- `omnichannel_subscription_imported`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_imported.md
- `omnichannel_subscription_moved_in`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_moved_in.md

### omnichannel_subscription_item

- `omnichannel_subscription_item_cancellation_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_cancellation_scheduled.md
- `omnichannel_subscription_item_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_cancelled.md
- `omnichannel_subscription_item_change_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_change_scheduled.md
- `omnichannel_subscription_item_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_changed.md
- `omnichannel_subscription_item_downgraded`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_downgraded.md
- `omnichannel_subscription_item_dunning_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_dunning_expired.md
- `omnichannel_subscription_item_dunning_started`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_dunning_started.md
- `omnichannel_subscription_item_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_expired.md
- `omnichannel_subscription_item_grace_period_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_grace_period_expired.md
- `omnichannel_subscription_item_grace_period_started`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_grace_period_started.md
- `omnichannel_subscription_item_mrr_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_mrr_updated.md
- `omnichannel_subscription_item_pause_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_pause_scheduled.md
- `omnichannel_subscription_item_paused`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_paused.md
- `omnichannel_subscription_item_reactivated`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_reactivated.md
- `omnichannel_subscription_item_recovered`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_recovered.md
- `omnichannel_subscription_item_renewed`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_renewed.md
- `omnichannel_subscription_item_resubscribed`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_resubscribed.md
- `omnichannel_subscription_item_resumed`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_resumed.md
- `omnichannel_subscription_item_scheduled_cancellation_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_scheduled_cancellation_removed.md
- `omnichannel_subscription_item_scheduled_change_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_scheduled_change_removed.md
- `omnichannel_subscription_item_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_updated.md
- `omnichannel_subscription_item_upgraded`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_subscription_item_upgraded.md

### omnichannel_transaction

- `omnichannel_transaction_created`: https://apidocs.chargebee.com/docs/api/events/webhook/omnichannel_transaction_created.md

### order

- `order_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/order_cancelled.md
- `order_created`: https://apidocs.chargebee.com/docs/api/events/webhook/order_created.md
- `order_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/order_deleted.md
- `order_delivered`: https://apidocs.chargebee.com/docs/api/events/webhook/order_delivered.md
- `order_ready_to_process`: https://apidocs.chargebee.com/docs/api/events/webhook/order_ready_to_process.md
- `order_ready_to_ship`: https://apidocs.chargebee.com/docs/api/events/webhook/order_ready_to_ship.md
- `order_resent`: https://apidocs.chargebee.com/docs/api/events/webhook/order_resent.md
- `order_returned`: https://apidocs.chargebee.com/docs/api/events/webhook/order_returned.md
- `order_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/order_updated.md

### organization_details

- `organization_details_created`: https://apidocs.chargebee.com/docs/api/events/webhook/organization_details_created.md
- `organization_details_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/organization_details_updated.md

### payment

- `payment_due_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_due_reminder.md
- `payment_failed`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_failed.md
- `payment_initiated`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_initiated.md
- `payment_refunded`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_refunded.md
- `payment_schedules_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_schedules_cancelled.md
- `payment_schedules_created`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_schedules_created.md
- `payment_schedules_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_schedules_updated.md
- `payment_succeeded`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_succeeded.md

### payment_intent

- `payment_intent_created`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_intent_created.md
- `payment_intent_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_intent_updated.md

### payment_schedule

- `payment_schedule_scheme_created`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_schedule_scheme_created.md
- `payment_schedule_scheme_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_schedule_scheme_deleted.md

### payment_source

- `payment_source_added`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_added.md
- `payment_source_business_entity_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_business_entity_changed.md
- `payment_source_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_deleted.md
- `payment_source_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_expired.md
- `payment_source_expiring`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_expiring.md
- `payment_source_locally_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_locally_deleted.md
- `payment_source_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/payment_source_updated.md

### pending_invoice

- `pending_invoice_created`: https://apidocs.chargebee.com/docs/api/events/webhook/pending_invoice_created.md
- `pending_invoice_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/pending_invoice_updated.md

### price_ramp

- `price_ramp_created`: https://apidocs.chargebee.com/docs/api/events/webhook/price_ramp_created.md
- `price_ramp_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/price_ramp_deleted.md
- `price_ramp_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/price_ramp_updated.md

### price_variant

- `price_variant_created`: https://apidocs.chargebee.com/docs/api/events/webhook/price_variant_created.md
- `price_variant_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/price_variant_deleted.md
- `price_variant_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/price_variant_updated.md

### promotional_credits

- `promotional_credits_added`: https://apidocs.chargebee.com/docs/api/events/webhook/promotional_credits_added.md
- `promotional_credits_deducted`: https://apidocs.chargebee.com/docs/api/events/webhook/promotional_credits_deducted.md

### purchase

- `purchase_created`: https://apidocs.chargebee.com/docs/api/events/webhook/purchase_created.md

### quote

- `quote_created`: https://apidocs.chargebee.com/docs/api/events/webhook/quote_created.md
- `quote_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/quote_deleted.md
- `quote_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/quote_updated.md

### refund

- `refund_failed`: https://apidocs.chargebee.com/docs/api/events/webhook/refund_failed.md
- `refund_initiated`: https://apidocs.chargebee.com/docs/api/events/webhook/refund_initiated.md

### rule

- `rule_created`: https://apidocs.chargebee.com/docs/api/events/webhook/rule_created.md
- `rule_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/rule_deleted.md
- `rule_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/rule_updated.md

### sales_order

- `sales_order_created`: https://apidocs.chargebee.com/docs/api/events/webhook/sales_order_created.md
- `sales_order_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/sales_order_updated.md

### subscription

- `subscription_activated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_activated.md
- `subscription_activated_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_activated_with_backdating.md
- `subscription_advance_invoice_schedule_added`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_advance_invoice_schedule_added.md
- `subscription_advance_invoice_schedule_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_advance_invoice_schedule_removed.md
- `subscription_advance_invoice_schedule_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_advance_invoice_schedule_updated.md
- `subscription_business_entity_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_business_entity_changed.md
- `subscription_canceled_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_canceled_with_backdating.md
- `subscription_cancellation_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_cancellation_reminder.md
- `subscription_cancellation_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_cancellation_scheduled.md
- `subscription_cancelled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_cancelled.md
- `subscription_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_changed.md
- `subscription_changed_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_changed_with_backdating.md
- `subscription_changes_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_changes_scheduled.md
- `subscription_created`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_created.md
- `subscription_created_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_created_with_backdating.md
- `subscription_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_deleted.md
- `subscription_items_renewed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_items_renewed.md
- `subscription_moved_in`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_moved_in.md
- `subscription_moved_out`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_moved_out.md
- `subscription_movement_failed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_movement_failed.md
- `subscription_pause_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_pause_scheduled.md
- `subscription_paused`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_paused.md
- `subscription_reactivated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_reactivated.md
- `subscription_reactivated_with_backdating`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_reactivated_with_backdating.md
- `subscription_renewal_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_renewal_reminder.md
- `subscription_renewed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_renewed.md
- `subscription_resumed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_resumed.md
- `subscription_resumption_scheduled`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_resumption_scheduled.md
- `subscription_scheduled_cancellation_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_scheduled_cancellation_removed.md
- `subscription_scheduled_changes_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_scheduled_changes_removed.md
- `subscription_scheduled_pause_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_scheduled_pause_removed.md
- `subscription_scheduled_resumption_removed`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_scheduled_resumption_removed.md
- `subscription_shipping_address_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_shipping_address_updated.md
- `subscription_started`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_started.md
- `subscription_trial_end_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_trial_end_reminder.md
- `subscription_trial_extended`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_trial_extended.md

### subscription_entitlements

- `subscription_entitlements_created`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_entitlements_created.md
- `subscription_entitlements_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_entitlements_updated.md

### subscription_ramp

- `subscription_ramp_applied`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_ramp_applied.md
- `subscription_ramp_created`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_ramp_created.md
- `subscription_ramp_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_ramp_deleted.md
- `subscription_ramp_drafted`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_ramp_drafted.md
- `subscription_ramp_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/subscription_ramp_updated.md

### tax_withheld

- `tax_withheld_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/tax_withheld_deleted.md
- `tax_withheld_recorded`: https://apidocs.chargebee.com/docs/api/events/webhook/tax_withheld_recorded.md
- `tax_withheld_refunded`: https://apidocs.chargebee.com/docs/api/events/webhook/tax_withheld_refunded.md

### token

- `token_consumed`: https://apidocs.chargebee.com/docs/api/events/webhook/token_consumed.md
- `token_created`: https://apidocs.chargebee.com/docs/api/events/webhook/token_created.md
- `token_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/token_expired.md

### transaction

- `transaction_created`: https://apidocs.chargebee.com/docs/api/events/webhook/transaction_created.md
- `transaction_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/transaction_deleted.md
- `transaction_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/transaction_updated.md

### unbilled_charges

- `unbilled_charges_created`: https://apidocs.chargebee.com/docs/api/events/webhook/unbilled_charges_created.md
- `unbilled_charges_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/unbilled_charges_deleted.md
- `unbilled_charges_invoiced`: https://apidocs.chargebee.com/docs/api/events/webhook/unbilled_charges_invoiced.md
- `unbilled_charges_voided`: https://apidocs.chargebee.com/docs/api/events/webhook/unbilled_charges_voided.md

### usage

- `usage_file_ingested`: https://apidocs.chargebee.com/docs/api/events/webhook/usage_file_ingested.md

### vault_token

- `vault_token_created`: https://apidocs.chargebee.com/docs/api/events/webhook/vault_token_created.md
- `vault_token_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/vault_token_deleted.md
- `vault_token_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/vault_token_updated.md

### virtual_bank_account

- `virtual_bank_account_added`: https://apidocs.chargebee.com/docs/api/events/webhook/virtual_bank_account_added.md
- `virtual_bank_account_deleted`: https://apidocs.chargebee.com/docs/api/events/webhook/virtual_bank_account_deleted.md
- `virtual_bank_account_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/virtual_bank_account_updated.md

### voucher

- `voucher_create_failed`: https://apidocs.chargebee.com/docs/api/events/webhook/voucher_create_failed.md
- `voucher_created`: https://apidocs.chargebee.com/docs/api/events/webhook/voucher_created.md
- `voucher_expired`: https://apidocs.chargebee.com/docs/api/events/webhook/voucher_expired.md

### other

- `add_usages_reminder`: https://apidocs.chargebee.com/docs/api/events/webhook/add_usages_reminder.md
- `alert_status_changed`: https://apidocs.chargebee.com/docs/api/events/webhook/alert_status_changed.md
- `dunning_updated`: https://apidocs.chargebee.com/docs/api/events/webhook/dunning_updated.md
- `email_message_received`: https://apidocs.chargebee.com/docs/api/events/webhook/email_message_received.md
- `private_note_added`: https://apidocs.chargebee.com/docs/api/events/webhook/private_note_added.md
- `record_purchase_failed`: https://apidocs.chargebee.com/docs/api/events/webhook/record_purchase_failed.md
- `retry_segment_assigned`: https://apidocs.chargebee.com/docs/api/events/webhook/retry_segment_assigned.md
