# MEANINGFRAME — ANALYTICS, VALIDATION & QA

## 1. Validation questions

The MVP must answer:

1. Do visitors understand the proposition?
2. Will they invest 6–9 minutes in the Co-Author Session?
3. Does the Meaning Map feel accurate and valuable?
4. Does the personal preview create a meaningful “wow” moment?
5. Will customers pay CHF 49 or CHF 229?
6. Which Art World performs best?
7. How much revision is required?
8. Can physical orders be fulfilled with acceptable quality and margin?
9. Will customers recommend or share the experience?
10. Does privacy messaging increase trust?

## 2. Event taxonomy

All events use allow-listed non-sensitive properties.

### Acquisition

- `landing_viewed`
- `example_viewed`
- `pricing_viewed`
- `primary_cta_clicked`

Properties:

- locale;
- campaign/source/medium;
- landing variant;
- device family.

### Session

- `project_started`
- `occasion_selected`
- `session_stage_started`
- `session_stage_completed`
- `session_resumed`
- `session_abandoned`
- `photo_upload_completed`
- `email_verification_requested`
- `email_verified`

Never send answer text, subject name or photo metadata to analytics.

### Meaning and preview

- `meaning_map_generated`
- `meaning_map_edited`
- `meaning_map_confirmed`
- `art_world_selected`
- `preview_requested`
- `preview_ready`
- `preview_viewed`
- `preview_technical_replacement`

Properties may include:

- art world;
- number of map edits;
- generation latency bucket;
- safe error code.

### Commerce

- `checkout_started`
- `checkout_cancelled`
- `payment_confirmed`
- `edition_purchased`
- `additional_revision_purchased`
- `atelier_review_purchased`

Use internal order reference, not payment/card data.

### Paid project

- `variants_ready`
- `variant_selected`
- `revision_submitted`
- `revision_ready`
- `curator_voice_selected`
- `final_approved`
- `deliverables_downloaded`
- `reveal_link_created`
- `reveal_viewed`

### Fulfilment

- `fulfilment_ready`
- `fulfilment_submitted`
- `fulfilment_shipped`
- `fulfilment_delivered`
- `fulfilment_incident`
- `refund_recorded`
- `reprint_recorded`

### Satisfaction

- `satisfaction_submitted`
- `referral_link_used`
- `share_opt_in`

## 3. Funnel dashboard

Required:

```text
Landing
→ Session start
→ Meaning Map
→ Confirmed Meaning Map
→ Preview
→ Checkout
→ Payment
→ Variants
→ Final approval
→ Delivery
```

Segments:

- occasion;
- locale;
- Art World;
- edition;
- acquisition source;
- new/returning;
- device family.

Minimum privacy rule: do not expose a segmented cell so small that it identifies a customer in normal staff use.

## 4. Quality dashboard

Track:

- schema failure rate;
- unsupported-claim QA rate;
- free-preview technical failure;
- paid-variant completion;
- average generation cost;
- p50/p95 generation latency;
- provider retry rate;
- likeness satisfaction;
- revision rate;
- additional revision rate;
- artwork approval time;
- refund/reprint/incident;
- physical contribution margin;
- deletion-job success.

## 5. First-impression test

Test at least five people unfamiliar with the product.

Within ten seconds ask:

- What does it do?
- Why might someone care?
- What would you receive?
- Is the first preview free?
- What happens to photos?

Score:

- understanding 0–100;
- first emotion;
- likelihood to continue 0–100;
- trust 0–100.

Release target:

- median understanding ≥ 80;
- no participant believes it is a generic photo filter;
- no participant believes a human artist paints every piece.

## 6. Moment-of-truth audit

Identify and test:

- strongest curiosity moment;
- strongest trust moment;
- strongest wow moment;
- strongest purchase moment;
- strongest recipient/reveal moment;
- strongest referral moment.

If any is absent, document a product gap before adding arbitrary features.

## 7. Price validation

Do not immediately discount the product.

Test:

- Digital CHF 49;
- Signature CHF 229;
- optional limited founder/beta offer with explicit reason.

Measure:

- checkout initiation;
- payment completion;
- edition mix;
- perceived fairness;
- expectation versus satisfaction;
- margin after actual cost.

Changing price requires a recorded experiment version.

## 8. User-test plan

### Round 1 — Prototype comprehension

- 5 participants
- landing, sample, start and fixed-question session
- no live AI required

### Round 2 — End-to-end beta

- 8–12 Co-Authors
- real stories and consented photos
- all Art Worlds represented
- test Stripe mode
- manual observation and interview

### Round 3 — Paid controlled launch

- first 10–20 real orders
- real price
- at least five Signature orders before scaling ads
- founder/operations review of every physical order

## 9. Satisfaction survey

After final approval:

- “The artwork feels recognisably personal.” 1–5
- “The Meaning Map reflected the person accurately.” 1–5
- “The Curator’s Note added value.” 1–5
- “The result feels worth the price.” 1–5
- “How likely are you to recommend MEANINGFRAME?” 0–10
- optional improvement text

After physical delivery:

- print quality;
- frame quality;
- packaging;
- delivery;
- gift reaction;
- permission request for testimonial/showcase must be separate.

## 10. Test strategy

### Unit

- state transitions;
- entitlements;
- price allow-list;
- retention calculation;
- preflight calculation;
- schema validation;
- sanitisation;
- localisation helpers.

### Integration

- Supabase RLS;
- Stripe event idempotency;
- auth claim;
- private storage;
- job retry;
- provider adapters with recorded fixtures;
- deletion across data/storage.

### End-to-end

Required critical paths:

1. DE Digital purchase;
2. EN Digital purchase;
3. Signature purchase black frame;
4. Signature purchase natural frame;
5. included revision;
6. additional paid revision;
7. payment webhook delay;
8. generation retry;
9. admin production bundle and shipment;
10. user immediate deletion;
11. unauthorised cross-account access denial;
12. prohibited-content block.

No live paid AI calls in normal CI. Use contract-faithful fixtures and a separate opt-in smoke suite.

## 11. Visual QA

Test widths:

- 360 px;
- 390 px;
- 768 px;
- 1024 px;
- 1440 px.

Review:

- no cropped primary action;
- artwork aspect ratio stable;
- zoom works;
- long German strings;
- focus and keyboard;
- loading and errors;
- email and PDF rendering;
- print PDF manually inspected.

## 12. AI evaluation

Run the fixture set in `07_AI_ORCHESTRATION_AND_PROMPTS.md`.

Release thresholds:

- 100% schema validity after permitted repair;
- zero unsupported sensitive inference;
- zero named artist prompt leakage;
- zero customer data in logs;
- ≥ 90% factual fidelity on manual evidence audit;
- all blocked fixtures remain blocked.

## 13. Security QA

Before launch:

- RLS negative tests;
- signed URL expiry;
- direct-object-reference tests;
- admin role tests;
- webhook replay;
- rate-limit tests;
- upload polyglot/corrupt/image-bomb cases;
- SVG XSS cases;
- secret scan;
- dependency audit;
- CSP review;
- deletion proof;
- backup restore rehearsal.

## 14. Launch gates

### Gate A — Product

- full paid journey works in DE and EN;
- no placeholder/TODO in production path;
- preview, variants, revision and final delivery proven;
- Signature admin workflow proven.

### Gate B — Quality

- sample print and frame approved;
- Curator’s Note print approved;
- AI evaluation passes;
- accessibility critical path passes.

### Gate C — Trust

- legal pages configured;
- consent/retention works;
- no public buckets;
- AI disclosure visible;
- vendor register complete.

### Gate D — Operations

- support inbox active;
- incident/refund/reprint runbooks ready;
- cost alerts ready;
- fulfilment owner named;
- test/production Stripe separation proven.

### Gate E — Commercial

- pricing matches checkout;
- five-user first-impression target met;
- controlled paid beta plan ready;
- no ad scale before early order review.

## 15. Weekly founder report

One-page output:

- traffic and funnel;
- orders/revenue/edition mix;
- generation cost/quality;
- revisions/refunds;
- physical operations;
- top three customer insights;
- top three issues;
- decisions required;
- scope and budget status.

