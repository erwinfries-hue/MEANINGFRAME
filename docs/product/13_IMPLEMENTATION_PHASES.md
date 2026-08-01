# MEANINGFRAME — CONTROLLED IMPLEMENTATION PHASES

## Global phase rule

- Execute one phase at a time.
- Do not begin the next phase without explicit founder approval.
- End every phase with an evidence report.
- Do not hide failed tests.
- Do not use mock success in a path declared complete.
- Update `docs/implementation/STATUS.md`, `DECISIONS.md`, `RISKS.md` and `COST_LEDGER.md`.

## Phase 0 — Repository, verification and build plan

### Objective

Understand the product package, inspect the repository and produce an executable implementation plan without building product features.

### Actions

1. Read every file under `docs/product/` completely.
2. Inspect repository, current code, config, Git status and existing instructions.
3. Check for `.openai/hosting.json`; if present, stop and report because Sites hosting rules may apply.
4. Verify current official documentation for:
   - Next.js/Vercel;
   - Supabase Auth/Postgres/Storage/RLS;
   - Anthropic native API and Structured Outputs;
   - Recraft raster/vector/image-to-image API;
   - Stripe Checkout/webhooks;
   - Inngest;
   - Resend.
5. Recommend exact pinned versions and model configuration.
6. Create:
   - `docs/implementation/IMPLEMENTATION_PLAN.md`
   - `docs/implementation/STATUS.md`
   - `docs/implementation/DECISIONS.md`
   - `docs/implementation/RISKS.md`
   - `docs/implementation/COST_LEDGER.md`
   - `docs/implementation/VENDOR_REGISTER.md`
   - `docs/implementation/REQUIREMENTS_TRACEABILITY.md`
7. Map every MVP requirement ID to a phase/test.
8. List all accounts, keys, business details and print samples required from founder.
9. Identify conflicts/blockers.
10. Propose the Phase 1 file changes.

### Prohibited

- no feature implementation;
- no database creation;
- no vendor account mutation;
- no production deployment;
- no paid-plan activation;
- no fabricated keys;
- no silent scope changes.

### Exit evidence

- repository assessment;
- official-doc verification links/date;
- pinned stack proposal;
- requirement traceability;
- risk register;
- cost/dependency ledger;
- Phase 1 plan;
- explicit `READY / NOT READY`.

Then stop.

## Phase 1 — Foundation, brand and secure project shell

### Objective

Build a production-quality application foundation.

### Scope

- initialise/pin project;
- strict TypeScript;
- code quality and CI;
- DE/EN routing;
- design tokens and brand shell;
- public pages with approved copy;
- Supabase local/migration structure;
- passwordless auth;
- anonymous project claim;
- private storage foundations;
- security headers;
- environment validation;
- first RLS tests;
- health/status endpoint;
- preview/staging deployment only.

### Exit

- home/pricing/example/privacy shell responsive;
- auth/claim works;
- user cannot access another project;
- CI green;
- no production deploy.

## Phase 2 — Co-Author Session and Meaning Map

### Objective

Complete the meaning-first customer foundation without image generation.

### Scope

- project lifecycle through Meaning Map confirmation;
- fixed question bank;
- adaptive follow-up adapter with fixtures;
- autosave/resume;
- secure image upload/sanitisation;
- photo observation;
- Meaning Map structured output;
- evidence mapping;
- edit and confirmation;
- internal admin diagnostic view;
- event tracking.

### Exit

- DE/EN session;
- real Claude staging smoke test;
- schema validation;
- no unsupported fact in fixture audit;
- raw personal data absent from logs;
- confirmed Meaning Map immutable.

## Phase 3 — Art Worlds and free preview

### Objective

Deliver the pre-purchase wow moment safely and economically.

### Scope

- Art World selection/recommendation;
- Art Brief structured output;
- Recraft adapter;
- raster and vector paths;
- one-preview entitlement;
- email-verification gate;
- abuse controls/rate limits;
- watermark derivative;
- job progress/retry;
- automated QA;
- preview UI and purchase CTA.

### Exit

- all three Art Worlds demonstrated with fixtures;
- one live staging call per output mode;
- watermark protection;
- rate-limit/idempotency test;
- cost captured;
- technical replacement path proven.

## Phase 4 — Stripe and paid variants

### Objective

Make the Digital and Signature products genuinely purchasable.

### Scope

- Stripe products/prices config;
- Digital/Signature checkout;
- frame choice/address;
- webhook verification/idempotency;
- order/entitlement ledger;
- three paid variants;
- variant comparison/selection;
- paid job recovery;
- confirmation emails;
- payment state/admin diagnostics.

### Exit

- test-mode Digital and Signature orders;
- webhook replay safe;
- success URL cannot grant access;
- three valid variants;
- cost/order reporting.

## Phase 5 — Revision, finalisation and digital delivery

### Objective

Complete the paid creative journey.

### Scope

- guided revision;
- included entitlement;
- CHF 19 revision checkout;
- Curator’s Note voices;
- note review;
- final approval;
- raster/vector final production;
- PDFs;
- Certificate;
- Reveal Page;
- secure downloads;
- retention countdown.

### Exit

- included/paid revision tests;
- final version approval binding;
- valid deliverable bundle;
- private Reveal Page revoke/expiry;
- PDF visual QA.

## Phase 6 — Signature fulfilment and operations

### Objective

Make the first 30–50 physical orders safely operable.

### Scope

- provider sample decision documented;
- final production spec configured;
- production preflight;
- production manifest;
- bundle ZIP;
- admin queue/status;
- provider ID/cost/tracking;
- customer status emails;
- incident/reprint/refund records;
- physical margin report.

### Exit

- internal test order reaches shipped state;
- bundle matches approved provider spec;
- no raw photos/story in bundle;
- operator runbook complete;
- sample product signed off.

## Phase 7 — Privacy, safety, analytics and hardening

### Objective

Prove launch trust and operational resilience.

### Scope

- consent ledger;
- retention/deletion jobs;
- immediate deletion/export;
- AI marking/disclosure;
- legal page configuration;
- vendor register finalisation;
- funnel/quality dashboards;
- alerts;
- backup/restore;
- security tests;
- accessibility;
- performance;
- incident runbooks.

### Exit

- launch Gates B–D pass;
- deletion evidence;
- RLS/security tests;
- WCAG critical path;
- no critical/high unresolved finding.

## Phase 8 — Controlled launch

### Objective

Launch to a small real Swiss audience and measure the business.

### Scope

- production environment;
- own domain;
- real Stripe;
- production AI keys;
- smoke transaction;
- first-impression test;
- 8–12 beta Co-Authors;
- first paid orders;
- weekly founder report;
- issue triage.

### Scaling restriction

Do not scale advertising until:

- at least ten paid projects;
- at least five Signature orders or founder override;
- print/revision/refund signals reviewed;
- cost/margin data complete;
- no unresolved privacy/security incident.

## Phase continuation prompts

After approving a phase, the founder can use:

```text
Read docs/product/ and the current docs/implementation/ records again.
Execute Phase [N] from docs/product/13_IMPLEMENTATION_PHASES.md only.
Preserve every binding decision and scope rule.
Implement, test and verify all Phase [N] exit criteria.
Update the implementation records and stop with a concise evidence report.
Do not begin Phase [N+1].
```

