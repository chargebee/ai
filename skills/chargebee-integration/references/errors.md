# Errors

Gateway error codes, sorted by code. Each links to a page with the root cause and possible solutions. The error response format and retry guidance are at https://apidocs.chargebee.com/docs/api/error-handling.md, and the full list is at https://apidocs.chargebee.com/docs/api/errors.md.


## gateway.bank_account

- `gateway.bank_account.account_activity_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_activity_exceeded.md
- `gateway.bank_account.account_b2b_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_b2b_issue.md
- `gateway.bank_account.account_blocked`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_blocked.md
- `gateway.bank_account.account_closed`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_closed.md
- `gateway.bank_account.account_config`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_config.md
- `gateway.bank_account.account_currency_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_currency_issue.md
- `gateway.bank_account.account_declined`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_declined.md
- `gateway.bank_account.account_frozen`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_frozen.md
- `gateway.bank_account.account_holder_deceased`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_holder_deceased.md
- `gateway.bank_account.account_restricted`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_restricted.md
- `gateway.bank_account.account_unusable`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_unusable.md
- `gateway.bank_account.account_unverified`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.account_unverified.md
- `gateway.bank_account.country_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.country_not_supported.md
- `gateway.bank_account.holder_name_length_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.holder_name_length_exceeded.md
- `gateway.bank_account.invalid_account_number`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.invalid_account_number.md
- `gateway.bank_account.invalid_iban`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.invalid_iban.md
- `gateway.bank_account.invalid_owner_name`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.invalid_owner_name.md
- `gateway.bank_account.live_not_permitted`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.live_not_permitted.md
- `gateway.bank_account.no_account`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.no_account.md
- `gateway.bank_account.sepa_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.sepa_not_supported.md
- `gateway.bank_account.setup_amount`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.setup_amount.md
- `gateway.bank_account.setup_hierarchy`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.setup_hierarchy.md
- `gateway.bank_account.test_only`: https://apidocs.chargebee.com/docs/api/errors/gateway.bank_account.test_only.md

## gateway.compliance

- `gateway.compliance.creditor_name_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.compliance.creditor_name_issue.md
- `gateway.compliance.invalid_account_details`: https://apidocs.chargebee.com/docs/api/errors/gateway.compliance.invalid_account_details.md
- `gateway.compliance.invalid_account_number`: https://apidocs.chargebee.com/docs/api/errors/gateway.compliance.invalid_account_number.md
- `gateway.compliance.regulatory_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.compliance.regulatory_issue.md
- `gateway.compliance.unauthorized_debit`: https://apidocs.chargebee.com/docs/api/errors/gateway.compliance.unauthorized_debit.md

## gateway.dispute

- `gateway.dispute.cannot_refund`: https://apidocs.chargebee.com/docs/api/errors/gateway.dispute.cannot_refund.md
- `gateway.dispute.charge_disputed`: https://apidocs.chargebee.com/docs/api/errors/gateway.dispute.charge_disputed.md
- `gateway.dispute.charge_not_refundable`: https://apidocs.chargebee.com/docs/api/errors/gateway.dispute.charge_not_refundable.md
- `gateway.dispute.currency_mismatch`: https://apidocs.chargebee.com/docs/api/errors/gateway.dispute.currency_mismatch.md
- `gateway.dispute.debit_disputed`: https://apidocs.chargebee.com/docs/api/errors/gateway.dispute.debit_disputed.md

## gateway.fraud

- `gateway.fraud.account_fraud`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.account_fraud.md
- `gateway.fraud.acquirer_counterfeit`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.acquirer_counterfeit.md
- `gateway.fraud.card_fraud`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.card_fraud.md
- `gateway.fraud.identified`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.identified.md
- `gateway.fraud.illegal_transaction`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.illegal_transaction.md
- `gateway.fraud.security_violation`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.security_violation.md
- `gateway.fraud.suspected_fraud`: https://apidocs.chargebee.com/docs/api/errors/gateway.fraud.suspected_fraud.md

## gateway.general

- `gateway.general.could_not_process`: https://apidocs.chargebee.com/docs/api/errors/gateway.general.could_not_process.md
- `gateway.general.decline`: https://apidocs.chargebee.com/docs/api/errors/gateway.general.decline.md
- `gateway.general.failure`: https://apidocs.chargebee.com/docs/api/errors/gateway.general.failure.md
- `gateway.general.not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.general.not_supported.md
- `gateway.general.unknown`: https://apidocs.chargebee.com/docs/api/errors/gateway.general.unknown.md

## gateway.identity_verification

- `gateway.identity_verification.3ds_authentication_failure`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.3ds_authentication_failure.md
- `gateway.identity_verification.additional_auth_required`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.additional_auth_required.md
- `gateway.identity_verification.authentication_required`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.authentication_required.md
- `gateway.identity_verification.cardholder_kyc_failure`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.cardholder_kyc_failure.md
- `gateway.identity_verification.contact_details_required`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.contact_details_required.md
- `gateway.identity_verification.contactless_fallback`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.contactless_fallback.md
- `gateway.identity_verification.invalid_pin_lock`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.invalid_pin_lock.md
- `gateway.identity_verification.invalid_user_cred`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.invalid_user_cred.md
- `gateway.identity_verification.not_found`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.not_found.md
- `gateway.identity_verification.pin_required`: https://apidocs.chargebee.com/docs/api/errors/gateway.identity_verification.pin_required.md

## gateway.mandate

- `gateway.mandate.billing_agreement_cancelled`: https://apidocs.chargebee.com/docs/api/errors/gateway.mandate.billing_agreement_cancelled.md
- `gateway.mandate.billing_agreement_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.mandate.billing_agreement_issue.md
- `gateway.mandate.mandate_incorrect`: https://apidocs.chargebee.com/docs/api/errors/gateway.mandate.mandate_incorrect.md
- `gateway.mandate.recurring_exceeded_limit`: https://apidocs.chargebee.com/docs/api/errors/gateway.mandate.recurring_exceeded_limit.md

## gateway.merchant_account

- `gateway.merchant_account.authentication_failure`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.authentication_failure.md
- `gateway.merchant_account.authentication_required`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.authentication_required.md
- `gateway.merchant_account.cannot_process_live`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.cannot_process_live.md
- `gateway.merchant_account.country_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.country_not_supported.md
- `gateway.merchant_account.currency_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.currency_not_supported.md
- `gateway.merchant_account.invalid_credentials`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.invalid_credentials.md
- `gateway.merchant_account.invalid_merchant`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.invalid_merchant.md
- `gateway.merchant_account.only_test_charges_allowed`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.only_test_charges_allowed.md
- `gateway.merchant_account.payment_method_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.payment_method_not_supported.md
- `gateway.merchant_account.setup_merchant`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.setup_merchant.md
- `gateway.merchant_account.test_only`: https://apidocs.chargebee.com/docs/api/errors/gateway.merchant_account.test_only.md

## gateway.payment_method

- `gateway.payment_method.card_barred`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_barred.md
- `gateway.payment_method.card_blocked`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_blocked.md
- `gateway.payment_method.card_currency_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_currency_not_supported.md
- `gateway.payment_method.card_cvv_disabled`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_cvv_disabled.md
- `gateway.payment_method.card_deactivated`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_deactivated.md
- `gateway.payment_method.card_expired`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_expired.md
- `gateway.payment_method.card_inactive`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_inactive.md
- `gateway.payment_method.card_incorrect_cvv`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_incorrect_cvv.md
- `gateway.payment_method.card_incorrect_number`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_incorrect_number.md
- `gateway.payment_method.card_incorrect_zip`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_incorrect_zip.md
- `gateway.payment_method.card_invalid_expiry`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_invalid_expiry.md
- `gateway.payment_method.card_invalid_number`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_invalid_number.md
- `gateway.payment_method.card_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_issue.md
- `gateway.payment_method.card_limit_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_limit_exceeded.md
- `gateway.payment_method.card_lost`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_lost.md
- `gateway.payment_method.card_not_activated`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_not_activated.md
- `gateway.payment_method.card_number_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_number_issue.md
- `gateway.payment_method.card_pin_invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_pin_invalid.md
- `gateway.payment_method.card_pin_retries_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_pin_retries_exceeded.md
- `gateway.payment_method.card_purchase_type_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_purchase_type_not_supported.md
- `gateway.payment_method.card_revoked`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_revoked.md
- `gateway.payment_method.card_suspended`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_suspended.md
- `gateway.payment_method.card_temp_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_temp_issue.md
- `gateway.payment_method.card_type_not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.card_type_not_supported.md
- `gateway.payment_method.config`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.config.md
- `gateway.payment_method.gift_card_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.gift_card_issue.md
- `gateway.payment_method.gift_card_tag_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.gift_card_tag_issue.md
- `gateway.payment_method.invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.invalid.md
- `gateway.payment_method.invalid_format`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.invalid_format.md
- `gateway.payment_method.not_found`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.not_found.md
- `gateway.payment_method.not_supported`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.not_supported.md
- `gateway.payment_method.paypal_validation_failed`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.paypal_validation_failed.md
- `gateway.payment_method.setup_card`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.setup_card.md
- `gateway.payment_method.unactivated`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.unactivated.md
- `gateway.payment_method.unexpected_state`: https://apidocs.chargebee.com/docs/api/errors/gateway.payment_method.unexpected_state.md

## gateway.technical

- `gateway.technical.acquirer_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.acquirer_issue.md
- `gateway.technical.bank_account_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.bank_account_issue.md
- `gateway.technical.could_not_process`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.could_not_process.md
- `gateway.technical.encryption_error`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.encryption_error.md
- `gateway.technical.inconsistent_data`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.inconsistent_data.md
- `gateway.technical.invalid_creditor_info`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.invalid_creditor_info.md
- `gateway.technical.invalid_order_id`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.invalid_order_id.md
- `gateway.technical.invalid_request_encoding`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.invalid_request_encoding.md
- `gateway.technical.invalid_request_error`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.invalid_request_error.md
- `gateway.technical.invalid_transaction`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.invalid_transaction.md
- `gateway.technical.invalid_transaction_code`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.invalid_transaction_code.md
- `gateway.technical.issuer_inoperative`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.issuer_inoperative.md
- `gateway.technical.issuer_invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.issuer_invalid.md
- `gateway.technical.issuer_not_found`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.issuer_not_found.md
- `gateway.technical.issuer_offline`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.issuer_offline.md
- `gateway.technical.issuer_unavailable`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.issuer_unavailable.md
- `gateway.technical.missing_data`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.missing_data.md
- `gateway.technical.network_downtime`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.network_downtime.md
- `gateway.technical.processor_feature_unavailable`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.processor_feature_unavailable.md
- `gateway.technical.processor_network_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.processor_network_issue.md
- `gateway.technical.rate_limit_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.rate_limit_exceeded.md
- `gateway.technical.server_error`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.server_error.md
- `gateway.technical.temporary_processing_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.temporary_processing_issue.md
- `gateway.technical.timeout`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.timeout.md
- `gateway.technical.unauthorized`: https://apidocs.chargebee.com/docs/api/errors/gateway.technical.unauthorized.md

## gateway.token

- `gateway.token.token_in_use`: https://apidocs.chargebee.com/docs/api/errors/gateway.token.token_in_use.md

## gateway.transaction_authorization

- `gateway.transaction_authorization.already_captured`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.already_captured.md
- `gateway.transaction_authorization.auth_already_reversed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.auth_already_reversed.md
- `gateway.transaction_authorization.auth_code_invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.auth_code_invalid.md
- `gateway.transaction_authorization.auth_expired`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.auth_expired.md
- `gateway.transaction_authorization.auth_not_found`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.auth_not_found.md
- `gateway.transaction_authorization.authorization_revoked`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.authorization_revoked.md
- `gateway.transaction_authorization.card_capture`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.card_capture.md
- `gateway.transaction_authorization.card_restrictions`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.card_restrictions.md
- `gateway.transaction_authorization.debit_authorization_revoked`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.debit_authorization_revoked.md
- `gateway.transaction_authorization.debit_authorization_stopped`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.debit_authorization_stopped.md
- `gateway.transaction_authorization.debit_not_authorized`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.debit_not_authorized.md
- `gateway.transaction_authorization.declined`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.declined.md
- `gateway.transaction_authorization.do_not_honor`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.do_not_honor.md
- `gateway.transaction_authorization.do_not_retry`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.do_not_retry.md
- `gateway.transaction_authorization.payment_stopped`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.payment_stopped.md
- `gateway.transaction_authorization.pre_authorization_failure`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.pre_authorization_failure.md
- `gateway.transaction_authorization.temp_auth_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.temp_auth_issue.md
- `gateway.transaction_authorization.unauthorized_debit`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.unauthorized_debit.md
- `gateway.transaction_authorization.voice_auth_required`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_authorization.voice_auth_required.md

## gateway.transaction_processing

- `gateway.transaction_processing.address_not_matching`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.address_not_matching.md
- `gateway.transaction_processing.amount_invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.amount_invalid.md
- `gateway.transaction_processing.amount_mismatch`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.amount_mismatch.md
- `gateway.transaction_processing.amount_too_large`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.amount_too_large.md
- `gateway.transaction_processing.amount_too_small`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.amount_too_small.md
- `gateway.transaction_processing.avs_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.avs_issue.md
- `gateway.transaction_processing.bin_invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.bin_invalid.md
- `gateway.transaction_processing.card_declined`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.card_declined.md
- `gateway.transaction_processing.cardholder_billing_stop`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.cardholder_billing_stop.md
- `gateway.transaction_processing.charge_already_refunded`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.charge_already_refunded.md
- `gateway.transaction_processing.charge_exceeds_source_limit`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.charge_exceeds_source_limit.md
- `gateway.transaction_processing.charge_invalid_parameter`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.charge_invalid_parameter.md
- `gateway.transaction_processing.charge_not_refundable`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.charge_not_refundable.md
- `gateway.transaction_processing.could_not_process`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.could_not_process.md
- `gateway.transaction_processing.decline_rate_limit_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.decline_rate_limit_exceeded.md
- `gateway.transaction_processing.duplicate_transaction`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.duplicate_transaction.md
- `gateway.transaction_processing.gift_no_balance`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.gift_no_balance.md
- `gateway.transaction_processing.incorrect_processing`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.incorrect_processing.md
- `gateway.transaction_processing.insufficient_funds`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.insufficient_funds.md
- `gateway.transaction_processing.invalid_account_number`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_account_number.md
- `gateway.transaction_processing.invalid_address`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_address.md
- `gateway.transaction_processing.invalid_config`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_config.md
- `gateway.transaction_processing.invalid_currency`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_currency.md
- `gateway.transaction_processing.invalid_level3_data`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_level3_data.md
- `gateway.transaction_processing.invalid_status`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_status.md
- `gateway.transaction_processing.invalid_transaction`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.invalid_transaction.md
- `gateway.transaction_processing.low_balance`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.low_balance.md
- `gateway.transaction_processing.network_decline`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.network_decline.md
- `gateway.transaction_processing.no_universal_account`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.no_universal_account.md
- `gateway.transaction_processing.not_permitted`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.not_permitted.md
- `gateway.transaction_processing.odfi_returned`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.odfi_returned.md
- `gateway.transaction_processing.over_max_balance`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.over_max_balance.md
- `gateway.transaction_processing.partial_refund_declined`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.partial_refund_declined.md
- `gateway.transaction_processing.payment_attempt_failed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_attempt_failed.md
- `gateway.transaction_processing.payment_code_incorrect`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_code_incorrect.md
- `gateway.transaction_processing.payment_intent_attempt_failed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_intent_attempt_failed.md
- `gateway.transaction_processing.payment_intent_invalid`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_intent_invalid.md
- `gateway.transaction_processing.payment_intent_mandate_inactive`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_intent_mandate_inactive.md
- `gateway.transaction_processing.payment_intent_unexpected_state`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_intent_unexpected_state.md
- `gateway.transaction_processing.payment_method_not_available`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_method_not_available.md
- `gateway.transaction_processing.payment_method_not_found`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_method_not_found.md
- `gateway.transaction_processing.payment_type_mismatch`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.payment_type_mismatch.md
- `gateway.transaction_processing.pickup_card_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.pickup_card_issue.md
- `gateway.transaction_processing.pickup_card_lost`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.pickup_card_lost.md
- `gateway.transaction_processing.processor_feature_unsupported`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.processor_feature_unsupported.md
- `gateway.transaction_processing.recurring_payment_mandate_canceled`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.recurring_payment_mandate_canceled.md
- `gateway.transaction_processing.refer_to_customer`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refer_to_customer.md
- `gateway.transaction_processing.refund_declined`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refund_declined.md
- `gateway.transaction_processing.refund_limit_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refund_limit_exceeded.md
- `gateway.transaction_processing.refund_not_allowed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refund_not_allowed.md
- `gateway.transaction_processing.refund_not_issued`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refund_not_issued.md
- `gateway.transaction_processing.refund_timelimit_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refund_timelimit_exceeded.md
- `gateway.transaction_processing.refund_window_crossed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.refund_window_crossed.md
- `gateway.transaction_processing.resource_missing`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.resource_missing.md
- `gateway.transaction_processing.surcharge_not_permitted`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.surcharge_not_permitted.md
- `gateway.transaction_processing.temp_not_allowed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.temp_not_allowed.md
- `gateway.transaction_processing.temporary_issue`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.temporary_issue.md
- `gateway.transaction_processing.transaction_expired`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.transaction_expired.md
- `gateway.transaction_processing.transaction_not_allowed`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.transaction_not_allowed.md
- `gateway.transaction_processing.transaction_not_permitted_to_cardholder`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.transaction_not_permitted_to_cardholder.md
- `gateway.transaction_processing.transaction_rejected`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.transaction_rejected.md
- `gateway.transaction_processing.unauthorized_debit`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.unauthorized_debit.md
- `gateway.transaction_processing.withdrawal_frequency_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.withdrawal_frequency_exceeded.md
- `gateway.transaction_processing.withdrawal_limit_exceeded`: https://apidocs.chargebee.com/docs/api/errors/gateway.transaction_processing.withdrawal_limit_exceeded.md
