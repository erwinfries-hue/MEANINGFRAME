# MEANINGFRAME — COMMERCE, FULFILMENT & OPERATIONS

## 1. Product catalogue

### DIGITAL_EDITION

- price: CHF 49
- one protected preview before purchase
- three refined variants
- one selection
- one included guided revision
- final digital artwork
- Curator’s Note PDF
- Certificate of Co-Creation PDF
- private Reveal Page
- personal-use licence

### SIGNATURE_EDITION_40X50

- price: CHF 229
- includes Digital Edition
- Fine Art print, 40 × 50 cm
- black or natural frame
- printed Curator’s Note
- Swiss standard delivery included

### ADDITIONAL_REVISION

- price: CHF 19
- one additional guided revision entitlement

### ATELIER_REVIEW

- price: CHF 49
- disclosed human review
- check likeness, composition, visible defects and print readiness
- review feedback and any approved corrective action recorded
- never sell if no qualified reviewer is operationally available

## 2. Price configuration

- Stripe Price IDs are environment-specific.
- Server has an allow-listed mapping from product code to price ID.
- UI reads price display from validated configuration or Stripe; it must not drift.
- Currency is CHF.
- Swiss tax treatment must be confirmed with the accountant and configured, not guessed in code.
- Any future EUR price is a separate market configuration.

## 3. Checkout

### Digital

Required inputs:

- authenticated project;
- confirmed Meaning Map;
- completed free preview;
- terms/privacy/AI acknowledgement.

### Signature

Additional:

- frame colour;
- Swiss delivery address;
- delivery estimate;
- personalised-goods and final-approval explanation.

Checkout metadata:

- project ID;
- internal product code;
- locale;
- immutable configuration version.

Do not put personal story content in Stripe metadata.

## 4. Fulfilment strategy

For the first 30–50 physical orders:

- customer experience is fully online;
- payment and order tracking are integrated;
- submission to the print provider is manual through admin operations;
- actual provider cost and issue data are captured;
- no customer-facing claim of full automation.

This is deliberate controlled fulfilment, not an incomplete product.

## 5. Print-provider selection

Before public physical launch:

1. shortlist Gelato and Prodigi or another approved provider;
2. obtain current Swiss production and shipping prices;
3. verify whether frame options match black/natural and 40 × 50 cm;
4. confirm Fine Art paper specification;
5. order identical samples from at least two candidates where practical;
6. evaluate colour, detail, frame, packaging, damage protection, branding and delivery;
7. document file requirements;
8. approve one primary provider and one operational fallback;
9. do not integrate an API in MVP.

Starting references:

- https://www.gelato.com/print-on-demand/switzerland
- https://www.prodigi.com/

## 6. Product specification

Final specification must be completed after sample approval:

| Attribute | Binding target |
|---|---|
| Finished art size | 40 × 50 cm |
| Frame colour | Black or natural |
| Artwork ratio | 4:5 |
| Paper | Approved Fine Art / museum-quality option |
| Glazing | Provider-defined and sample-approved |
| Curator’s Note | Premium heavyweight paper, separate presentation |
| Packaging | Gift-appropriate, damage-protective |
| Delivery | Swiss standard included |

If the print provider cannot insert the Curator’s Note, the operations runbook must define a controlled local assembly step or select a different fulfilment method. The customer promise must match the real operation.

## 7. Production preflight

Preflight blocks fulfilment unless all checks pass:

- order paid;
- final artwork approved;
- final Curator’s Note approved;
- correct 4:5 output/crop;
- required pixel dimensions/effective ppi or valid vector;
- colour profile matches provider rule;
- no unintended transparency/border;
- safe area confirmed;
- no watermark;
- no generated text/signature/logo;
- correct frame colour;
- delivery address complete;
- asset hashes recorded;
- production manifest validates.

## 8. Production bundle

ZIP name:

`MF-{orderReference}-production.zip`

Contents:

```text
artwork/
  MF-{orderReference}-artwork.{png|tif|pdf|svg}
curator-note/
  MF-{orderReference}-curator-note.pdf
reference/
  MF-{orderReference}-proof.jpg
manifest/
  production-manifest.json
```

Do not include:

- source photos;
- raw answers;
- Meaning Map evidence;
- customer email;
- unnecessary personal story.

Delivery address is handled in the order/admin view, not embedded in the art bundle unless the provider upload requires a separate minimal order file.

## 9. Manual operations states

1. `FULFILMENT_READY`
2. `PREFLIGHT_PASSED`
3. `SUBMITTED_TO_PROVIDER`
4. `IN_PRODUCTION`
5. `SHIPPED`
6. `DELIVERED`

Admin must record:

- operator;
- timestamp;
- provider;
- provider order ID;
- quoted/actual cost;
- shipping/tracking;
- exception.

## 10. Service expectations

Initial operational targets:

- paid generation dispatched within 5 minutes;
- paid variants normally available within 30 minutes, with honest exception handling;
- human Atelier Review within two Swiss business days;
- physical order submitted within one Swiss business day after customer approval;
- customer notified of significant delay;
- support response target: one Swiss business day.

Do not display hard delivery dates until provider performance is evidenced.

## 11. Customer communications

Required transactional messages:

- magic link;
- project saved/resume;
- personal preview ready;
- payment confirmation;
- refined variants ready;
- revision ready;
- final files ready;
- Signature order submitted/in production;
- shipped with tracking;
- delay/incident;
- retention/deletion reminder;
- deletion completed.

Email must not include private artwork by default. Use secure project links.

## 12. Quality incidents

### AI/content

- unrecognisable subject;
- missing required symbol;
- visible image defect;
- safety/moderation issue;
- wrong Art World;
- corrupted output.

### Physical

- colour deviation;
- crop problem;
- frame damage;
- print defect;
- missing Curator’s Note;
- lost shipment;
- wrong frame colour.

Every incident must capture:

- type;
- root-cause category;
- resolution;
- cost;
- whether provider, system or customer-input related;
- prevention action.

## 13. Refund and reprint authority

Admin roles must have documented limits. At minimum:

- technical generation failure: restore entitlement/retry;
- physical defect: reprint or refund according to approved policy;
- duplicate charge: reconcile/refund;
- goodwill: tracked separately.

Never delete the audit/payment record when refunding.

## 14. Margin reporting

Per order:

```text
net revenue
- Stripe/payment fee
- Claude cost
- Recraft cost
- storage/compute allocation
- PDF/email cost allocation
- print/framing
- shipping
- reprint/refund cost
= contribution before marketing
```

The dashboard must show actual vendor cost where available and identify missing cost data.

## 15. Fulfilment automation gate

Automate provider API only after:

- at least 30 successful physical orders or founder override;
- primary provider proven;
- file specification stable;
- reprint rate acceptable;
- manual steps documented;
- contribution margin validated;
- API error and idempotency design approved.

