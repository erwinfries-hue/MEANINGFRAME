# MEANINGFRAME — FUNCTIONAL REQUIREMENTS & ACCEPTANCE

Every `MUST` item is a release requirement unless explicitly assigned to a later phase.

## 1. Public product

### FR-PUB-001 — Product comprehension

The home page MUST communicate personal art, guided co-creation, free preview and privacy above the fold in DE and EN.

Acceptance:

- a first-time test participant can state what they receive and what happens before payment;
- primary CTA is visible at 360 px width without horizontal scrolling;
- content contains no false human-artist claim.

### FR-PUB-002 — Localisation

All customer-facing application strings MUST use translation keys.

Acceptance:

- locale switching preserves the current route and project;
- no mixed-language critical flow;
- prices remain CHF for both languages in Swiss pilot.

### FR-PUB-003 — Example project

The site MUST include a clearly fictional or consented example containing input summary, Meaning Map, preview/final artwork and Curator’s Note.

Acceptance:

- example content cannot be mistaken for a live customer;
- no unlicensed person or artist reference is used.

## 2. Identity and access

### FR-AUTH-001 — Passwordless access

A visitor MUST be able to begin before login and verify email by magic link before preview generation.

Acceptance:

- no password field;
- anonymous project transfers safely to verified account;
- another user cannot claim the project;
- expired links have a resend flow.

### FR-AUTH-002 — Project ownership

Every private project request MUST enforce owner or authorised admin access server-side.

Acceptance:

- direct object reference tests fail for other accounts;
- signed asset URLs are short-lived;
- service-role credentials never reach the browser.

## 3. Co-Author Session

### FR-SES-001 — Structured and adaptive session

The session MUST combine fixed required questions with no more than three AI-selected follow-ups.

Acceptance:

- required fields are explicit;
- optional questions are skippable;
- follow-ups include an internal reason code;
- a repeated or irrelevant follow-up is rejected by validation.

### FR-SES-002 — Autosave and resume

Answers MUST autosave without a submit-per-screen requirement.

Acceptance:

- refresh restores the latest saved state;
- network failure displays unsaved state;
- conflicting multi-tab edits are detected or last-write policy is explicit.

### FR-SES-003 — Uploads

The system MUST accept two to five optional photos in supported image formats.

Acceptance:

- MIME is verified by decoded content, not filename;
- EXIF is stripped;
- image is re-encoded server-side;
- unsupported/corrupt files are rejected;
- original assets are private;
- configured size and pixel limits are enforced;
- consent must be stored before use.

## 4. Meaning Map

### FR-MM-001 — Schema-constrained generation

Claude MUST return a Meaning Map conforming to `schemas/meaning-map.schema.json`.

Acceptance:

- invalid output is not persisted as confirmed;
- one automatic repair attempt is allowed;
- failure creates a recoverable error and diagnostic ID;
- facts are traceable to submitted answer IDs.

### FR-MM-002 — No invention

The Meaning Map MUST distinguish confirmed facts, Co-Author interpretations and artistic proposals.

Acceptance:

- sensitive or unsupported inferences are absent;
- confidence and missing information are represented;
- generated prose cannot add unprovided life events.

### FR-MM-003 — Confirmation and versioning

The Co-Author MUST confirm an immutable Meaning Map version before generation.

Acceptance:

- edits produce a new version;
- every image generation references one version ID;
- admin can trace output to version without exposing data to analytics.

## 5. Art generation

### FR-ART-001 — Provider abstraction

Image generation MUST be called through a typed provider interface.

Acceptance:

- provider keys and model IDs are environment configuration;
- application domain code has no Recraft-specific response shape;
- failure and cost data are normalised.

### FR-ART-002 — Free preview

The system MUST generate exactly one free protected preview per eligible project, except verified technical replacement.

Acceptance:

- email verified;
- Meaning Map confirmed;
- consent present;
- rate limiting passes;
- preview is watermarked and reduced resolution;
- original high-resolution provider output is private;
- request is idempotent.

### FR-ART-003 — Paid variants

A paid project MUST generate three meaningfully distinct refined variants.

Acceptance:

- variants share the confirmed identity and meaning;
- each has a distinct composition seed or art-direction variation;
- technical QA executes;
- failed individual variant retries without duplicating all successful variants;
- customer sees three valid variants or an honest incomplete state.

### FR-ART-004 — Output path

The system MUST produce native vector output for supported Modern Essence jobs and high-resolution raster output for painterly/collage jobs.

Acceptance:

- vector file is valid SVG and sanitised;
- raster meets configured print dimensions and minimum effective resolution;
- output contains no unintended generated text;
- print profile requirements are documented in manifest.

## 6. Commerce

### FR-PAY-001 — Stripe catalogue

The application MUST support Digital Edition, Signature Edition, additional revision and Atelier Review as configured Stripe prices.

Acceptance:

- server maps allow-listed price IDs to products;
- client cannot submit arbitrary price;
- test and production IDs are separated;
- price display matches checkout.

### FR-PAY-002 — Webhook authority

Payment state MUST be set only from verified Stripe webhooks or verified server retrieval.

Acceptance:

- signature verification;
- event idempotency;
- replay safe;
- delayed webhook state handled;
- no fulfilment before successful payment.

### FR-PAY-003 — Signature data

Signature order MUST collect frame colour and Swiss delivery address.

Acceptance:

- only black/natural valid;
- country restricted to configured pilot;
- address retained only as required for fulfilment/legal obligations;
- shipping included in configured price for standard Swiss delivery.

## 7. Selection and revision

### FR-REV-001 — Variant selection

The Co-Author MUST select one paid variant before revision/finalisation.

Acceptance:

- exactly one active selection;
- selection history retained;
- no unselected variant sent to production.

### FR-REV-002 — Included guided revision

Every paid edition MUST include one guided revision.

Acceptance:

- up to three structured categories;
- text length limited;
- revision modifies selected variant rather than starting unrelated work;
- entitlement decremented atomically;
- failed provider job does not consume entitlement.

### FR-REV-003 — Additional revision

Further revisions MUST require a CHF 19 successful payment.

Acceptance:

- entitlement added only by webhook;
- one payment equals one revision;
- unused entitlement visible.

## 8. Curator’s Note

### FR-NOTE-001 — Voice

The system MUST provide Personal & Warm, Poetic and Curatorial voices.

Acceptance:

- default is Personal & Warm;
- same confirmed facts across voices;
- no fake critic identity;
- unsupported facts rejected by schema/validation.

### FR-NOTE-002 — Review

The Co-Author MUST review the note before final approval.

Acceptance:

- factual correction path exists;
- final PDF uses approved version;
- editing cannot inject executable markup.

## 9. Finalisation and delivery

### FR-FIN-001 — Explicit approval

Final production MUST require explicit customer approval.

Acceptance:

- approval records version IDs, timestamp and actor;
- physical fulfilment is blocked until approval;
- later content changes create a new approval requirement.

### FR-FIN-002 — Delivery package

Digital delivery MUST include the valid final artwork, Curator’s Note PDF, Co-Creation Certificate PDF and private Reveal Page.

Acceptance:

- downloads require authorisation or unguessable revocable link;
- files have meaningful names;
- retention expiry shown;
- broken asset test fails release.

## 10. Fulfilment

### FR-FUL-001 — Manual production queue

Admin MUST see approved paid Signature orders awaiting fulfilment.

Acceptance:

- queue excludes unpaid/unapproved orders;
- status transition rules enforced;
- production bundle passes preflight before download.

### FR-FUL-002 — Provider record

Admin MUST record provider order ID, actual production cost, submission date and tracking.

Acceptance:

- status changes audited;
- customer receives appropriate notification;
- actual cost feeds margin reporting.

### FR-FUL-003 — Incidents

Admin MUST record reprint, refund, damage or delivery incident.

Acceptance:

- incident references order;
- financial impact stored;
- personal/sensitive narrative not copied into analytics.

## 11. Privacy

### FR-PRV-001 — Consent ledger

The system MUST store versioned consent records for photos, terms, privacy, AI use and final production approval.

### FR-PRV-002 — Retention engine

The system MUST calculate and execute raw-input and final-output deletion deadlines.

Acceptance:

- abandoned and purchased-project policies differ correctly;
- deletion covers database content, storage objects and derived prompt payloads under platform control;
- legal transaction records are minimised rather than indiscriminately deleted;
- failed deletion creates an alert and retry.

### FR-PRV-003 — User controls

The customer MUST be able to request immediate deletion and download core project data.

Acceptance:

- order/legal constraints explained;
- deletion requires re-authentication;
- status and completion confirmation available.

## 12. Admin and observability

### FR-ADM-001 — Role access

Admin routes MUST require an explicit admin role and server-side authorisation.

### FR-ADM-002 — AI diagnostics

Admin MUST see job state, provider, model, latency, cost, error code and safe diagnostic summary.

Raw personal prompts must not be shown by default.

### FR-OBS-001 — Operational logging

Logs MUST use correlation IDs and redact secrets, signed URLs, payment details and personal answers.

## 13. Non-functional requirements

### NFR-001 — Accessibility

WCAG 2.2 AA for the complete purchase path.

### NFR-002 — Performance

Targets on representative mobile:

- public LCP ≤ 2.5 seconds at p75;
- CLS ≤ 0.1;
- INP ≤ 200 ms where measured;
- no full-size customer image loaded into list views;
- upload progress visible.

AI generation is asynchronous and excluded from web response latency, but its status must remain observable.

### NFR-003 — Reliability

- idempotent payment and generation operations;
- retry with bounded exponential backoff;
- no duplicate physical order from replay;
- daily database backup capability verified;
- restoration runbook documented.

### NFR-004 — Security

- dependency and secret scanning in CI;
- least-privilege database access;
- Row Level Security;
- server-side input validation with Zod;
- CSRF-safe mutation patterns;
- rate limiting;
- CSP and secure headers;
- sanitised SVG;
- upload re-encoding;
- no secrets in client bundles.

### NFR-005 — Browser support

Latest two major versions of Chrome, Safari, Edge and Firefox; current iOS Safari and Android Chrome.

## 14. Definition of done

A feature is not done until:

- acceptance criteria pass;
- unit/integration/e2e coverage appropriate to risk exists;
- error and loading states exist;
- DE/EN copy exists;
- analytics event exists where specified;
- privacy/security review is complete;
- no TODO, mock or hard-coded test identity remains in production path;
- documentation and environment requirements are updated.

