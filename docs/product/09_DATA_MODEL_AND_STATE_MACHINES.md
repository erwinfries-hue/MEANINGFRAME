# MEANINGFRAME — DATA MODEL & STATE MACHINES

## 1. Data design principles

- UUID primary keys;
- UTC timestamps;
- explicit state enums/check constraints;
- immutable versions for confirmed/generated content;
- evidence references instead of untraceable prose;
- minimal personal data;
- no address duplication outside order/fulfilment need;
- soft deletion only where operationally required, followed by hard deletion according to policy;
- append-only consent and payment event records;
- Row Level Security on customer-owned tables.

## 2. Core tables

The exact SQL may vary, but all concepts below must be represented.

### `profiles`

- `user_id`
- `display_name` optional
- `preferred_locale`
- `role` customer/admin
- timestamps

Do not collect birth date, phone or postal address at account level in MVP.

### `projects`

- `id`
- `owner_user_id` nullable until claimed
- `anonymous_claim_hash` nullable
- `mode`
- `occasion`
- `locale`
- `subject_display_name`
- `state`
- `selected_art_world`
- `preview_entitlement_used_at`
- `raw_delete_after`
- `final_delete_after`
- timestamps

### `project_answers`

- `id`
- `project_id`
- `question_key`
- `answer_json`
- `sensitivity`
- `source` co_author/fixed_choice/dynamic_follow_up
- `dynamic_reason_code` nullable
- `version`
- timestamps

Keep evidence IDs stable across Meaning Map versions until source deletion.

### `project_assets`

- `id`
- `project_id`
- `owner_user_id`
- `kind` source_photo/sanitised_photo/preview/refined/final/note/certificate/production
- `storage_bucket`
- `storage_path`
- `mime_type`
- `bytes`
- `width`
- `height`
- `sha256`
- `safety_state`
- `delete_after`
- timestamps

### `photo_observations`

- `id`
- `asset_id`
- `schema_version`
- `model_id`
- `observation_json`
- `suitability_score`
- `delete_after`

### `consent_records`

- `id`
- `project_id`
- `user_id`
- `consent_type`
- `policy_version`
- `granted`
- `context_json` minimised
- `ip_hash` optional and short-retained
- `user_agent_family` optional
- `created_at`

Consent types:

- privacy_notice_acknowledged
- terms_accepted
- photo_use_confirmed
- ai_processing_acknowledged
- minor_guardian_confirmed
- immediate_digital_performance_eu_future
- final_production_approved
- voluntary_publication_opt_in

### `meaning_map_versions`

- `id`
- `project_id`
- `version_number`
- `schema_version`
- `content_json`
- `prompt_version`
- `model_id`
- `status` draft/confirmed/superseded
- `confirmed_by`
- `confirmed_at`
- timestamps

Confirmed versions are immutable.

### `art_briefs`

- `id`
- `project_id`
- `meaning_map_version_id`
- `art_world`
- `output_mode`
- `schema_version`
- `content_json`
- `prompt_version`
- `model_id`
- timestamps

### `generation_jobs`

- `id`
- `project_id`
- `job_type`
- `idempotency_key` unique
- `state`
- `attempt_count`
- `provider`
- `model_id`
- `prompt_version`
- `input_version_refs_json`
- `safe_error_code`
- `safe_error_summary`
- `provider_request_id` encrypted/restricted where appropriate
- `started_at`
- `completed_at`
- `cost_minor_usd`
- `duration_ms`
- timestamps

Do not store full raw provider payload indefinitely.

### `artwork_versions`

- `id`
- `project_id`
- `meaning_map_version_id`
- `art_brief_id`
- `generation_job_id`
- `kind` preview/refined/revision/final
- `variant_number` nullable
- `parent_artwork_version_id` nullable
- `asset_id`
- `qa_state`
- `qa_json`
- `selected_at` nullable
- timestamps

### `revisions`

- `id`
- `project_id`
- `source_artwork_version_id`
- `entitlement_source` included/paid/admin_recovery
- `change_categories`
- `instruction_text`
- `state`
- `result_artwork_version_id`
- timestamps

### `curator_note_versions`

- `id`
- `project_id`
- `meaning_map_version_id`
- `artwork_version_id`
- `voice`
- `schema_version`
- `content_json`
- `status` draft/approved/superseded
- `asset_id` nullable
- timestamps

### `approvals`

- `id`
- `project_id`
- `approval_type`
- `artwork_version_id`
- `curator_note_version_id`
- `user_id`
- `policy_version`
- `approved_at`

### `orders`

- `id`
- `order_reference`
- `project_id`
- `user_id`
- `state`
- `currency`
- `subtotal_minor`
- `tax_minor`
- `shipping_minor`
- `total_minor`
- `stripe_customer_id` restricted
- `stripe_checkout_session_id` restricted
- `paid_at`
- timestamps

### `order_items`

- `id`
- `order_id`
- `product_code`
- `quantity`
- `unit_price_minor`
- `frame_colour` nullable
- `entitlement_json`

Product codes:

- DIGITAL_EDITION
- SIGNATURE_EDITION_40X50
- ADDITIONAL_REVISION
- ATELIER_REVIEW

### `payment_events`

- `id`
- `provider_event_id` unique
- `event_type`
- `payload_reference_or_minimised_json`
- `processed_at`
- `processing_result`
- timestamps

### `fulfilments`

- `id`
- `order_id`
- `state`
- `provider_name`
- `provider_order_id`
- `actual_cost_minor`
- `cost_currency`
- `submitted_at`
- `shipped_at`
- `tracking_carrier`
- `tracking_number` encrypted/restricted
- `tracking_url` validated
- timestamps

### `fulfilment_incidents`

- `id`
- `fulfilment_id`
- `type` damage/lost/quality/reprint/refund/other
- `status`
- `safe_summary`
- `financial_impact_minor`
- timestamps

### `reveal_links`

- `id`
- `project_id`
- `token_hash`
- `revoked_at`
- `expires_at`
- `view_count`
- timestamps

Store only a token hash. Never store the raw share token after creation.

### `deletion_jobs`

- `id`
- `project_id`
- `scope`
- `scheduled_for`
- `state`
- `attempt_count`
- `result_json`
- timestamps

### `audit_events`

- `id`
- `actor_type`
- `actor_id` nullable
- `project_id` nullable
- `order_id` nullable
- `event_type`
- `safe_metadata_json`
- `created_at`

No raw answers, image URLs, card data or secret values.

### `product_events`

- `id`
- `anonymous_or_user_pseudonym`
- `project_id` nullable/pseudonymised
- `event_name`
- `properties_json` allow-listed
- `session_id`
- `occurred_at`
- `delete_after`

### `vendor_costs`

- `id`
- `project_id`
- `order_id` nullable
- `generation_job_id` nullable
- `vendor`
- `operation`
- `amount_minor`
- `currency`
- `occurred_at`

## 3. Project state machine

```text
DRAFT
  → SESSION_IN_PROGRESS
  → MEANING_MAP_DRAFT
  → MEANING_MAP_CONFIRMED
  → PREVIEW_QUEUED
  → PREVIEW_READY
  → CHECKOUT_PENDING
  → PAID
  → VARIANTS_QUEUED
  → VARIANTS_READY
  → VARIANT_SELECTED
  → REVISION_QUEUED (optional)
  → FINAL_REVIEW
  → APPROVED
  → DELIVERED
  → RETENTION_EXPIRED
  → DELETED
```

Exceptional states:

- `NEEDS_ADMIN_REVIEW`
- `BLOCKED_SAFETY`
- `PAYMENT_RECONCILIATION`
- `GENERATION_FAILED`
- `DELETION_FAILED`

Rules:

- transitions are enforced server-side;
- transition writes audit event;
- state cannot skip payment for paid capabilities;
- final approval references exact immutable versions;
- deletion is terminal except minimised legal/financial records.

## 4. Generation state machine

```text
PENDING → DISPATCHED → RUNNING → QA_PENDING → SUCCEEDED
                                ↘ RETRY_WAIT
                                ↘ NEEDS_REVIEW
                                ↘ FAILED
                                ↘ BLOCKED
```

Rules:

- successful idempotency key cannot create a second billable operation;
- retry uses the same logical job and records attempt;
- non-retryable moderation/safety failures do not loop;
- customer-safe errors reveal no provider internals.

## 5. Order state machine

```text
CREATED → CHECKOUT_OPEN → PAYMENT_PENDING → PAID
  → CONTENT_IN_PRODUCTION
  → CUSTOMER_APPROVAL_REQUIRED
  → APPROVED
  → DIGITAL_DELIVERED
```

Signature branch:

```text
APPROVED
  → FULFILMENT_READY
  → SUBMITTED_TO_PROVIDER
  → IN_PRODUCTION
  → SHIPPED
  → DELIVERED
```

Exceptional:

- CANCELLED
- REFUNDED
- PARTIALLY_REFUNDED
- DISPUTED
- FULFILMENT_INCIDENT

## 6. Revision entitlements

Represent entitlements as ledger entries or immutable order-item grants, not a mutable boolean.

Consumption transaction:

1. lock available entitlement;
2. create revision with entitlement reference;
3. mark entitlement reserved;
4. dispatch job;
5. consume only when valid result succeeds;
6. release reservation on terminal technical failure.

## 7. Retention calculation

### Unpurchased project

- source photos, free text, photo observations and provider payload derivatives: delete seven days after last activity;
- watermarked preview: delete 30 days after creation unless project is purchased;
- minimised anonymous funnel events: per analytics policy.

### Purchased project

- source photos, raw free text, photo observations and sensitive prompt payloads: delete 30 days after project completion/final approval;
- final artwork, Curator’s Note, Certificate and Reveal Page: retain 12 months from delivery;
- financial and legally required transaction records: retain according to accounting/legal policy, minimised and separated from creative inputs.

### Immediate deletion

- revoke reveal links and downloads promptly;
- delete creative input/output under platform control;
- preserve only required transaction/legal record with explanation.

## 8. RLS expectations

- customer can read/write own active project rows only;
- customer cannot directly mutate payment, admin, job, cost, audit or fulfilment state;
- storage policies mirror project ownership;
- reveal token access goes through server function, not broad storage RLS;
- admin service path is server-only;
- service role is never browser-accessible;
- automated RLS tests are required.

