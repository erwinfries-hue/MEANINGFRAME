# MEANINGFRAME — TECHNICAL ARCHITECTURE

## 1. Architecture goals

- productive rather than prototype-only;
- simple enough for an 8–10 week MVP;
- secure handling of personal photos and stories;
- recoverable asynchronous AI work;
- vendor replacement without rewriting product logic;
- DACH commerce readiness without activating non-Swiss markets;
- clear staging and production separation.

## 2. Proposed stack

Claude Code MUST verify current official documentation and stable versions during Phase 0, then pin exact versions.

| Layer | Default |
|---|---|
| Web framework | Current stable Next.js App Router with TypeScript strict mode |
| Package manager | `pnpm` |
| UI | Tailwind CSS plus accessible headless components; shadcn/ui allowed |
| Forms/validation | React Hook Form where useful plus Zod as shared schema layer |
| Localisation | `next-intl` or verified equivalent |
| Database | Supabase Postgres in an EU region |
| Auth | Supabase Auth magic links |
| Private storage | Supabase Storage private buckets |
| Hosting | Vercel |
| Background jobs | Inngest behind an internal `JobDispatcher` adapter |
| Text/vision AI | Native Anthropic API with Structured Outputs |
| Image AI | Recraft API behind `ImageGenerationProvider` |
| Payments | Stripe Checkout and webhooks |
| Transactional email | Resend behind `EmailProvider` |
| PDF | server-side deterministic PDF renderer such as `@react-pdf/renderer` |
| Image processing | `sharp` in supported server runtime |
| Product analytics | internal first-party event table; optional PostHog EU adapter without session replay |
| Error monitoring | structured logs; optional Sentry adapter |
| Tests | Vitest, Testing Library and Playwright |
| CI | GitHub Actions |

No provider may be added to production until its terms, data handling, region, cost and deletion implications are recorded in the vendor register.

## 3. System context

```text
Browser
  │
  ├── Public pages / authenticated project UI
  │
Vercel Next.js application
  ├── Supabase Auth
  ├── Supabase Postgres + RLS
  ├── Supabase private Storage
  ├── Inngest job dispatcher
  ├── Anthropic adapter
  ├── Recraft adapter
  ├── Stripe adapter/webhook
  └── Email adapter

Admin UI uses the same application with explicit server-side admin authorisation.
```

## 4. Architectural boundaries

### Domain layer

Contains:

- project lifecycle;
- Meaning Map versioning;
- entitlement and revision logic;
- order and fulfilment state rules;
- retention calculation;
- production preflight;
- pure validation.

The domain layer MUST NOT import vendor SDKs.

### Application services

Orchestrate use cases:

- start project;
- save answer;
- confirm Meaning Map;
- request preview;
- create checkout;
- handle paid order;
- request variants;
- submit revision;
- approve final;
- prepare production;
- delete project.

### Provider adapters

Typed interfaces:

```ts
interface TextIntelligenceProvider {
  createStructuredOutput<T>(request: StructuredTextRequest<T>): Promise<StructuredTextResult<T>>;
  observeImages(request: ImageObservationRequest): Promise<ImageObservationResult>;
}

interface ImageGenerationProvider {
  generateRaster(request: RasterGenerationRequest): Promise<ImageGenerationResult>;
  generateVector(request: VectorGenerationRequest): Promise<ImageGenerationResult>;
  imageToImage(request: ImageToImageRequest): Promise<ImageGenerationResult>;
  upscale(request: UpscaleRequest): Promise<ImageGenerationResult>;
}

interface PaymentProvider {}
interface EmailProvider {}
interface JobDispatcher {}
interface AnalyticsSink {}
interface FulfilmentProvider {}
```

`FulfilmentProvider` exists in MVP even though the default implementation is manual admin fulfilment. This prevents the later Gelato/Prodigi integration from leaking into order logic.

## 5. Repository structure

Suggested:

```text
app/
  [locale]/
    (marketing)/
    (project)/
    (account)/
    admin/
  api/
components/
  brand/
  ui/
  project/
  artwork/
domain/
  project/
  meaning-map/
  artwork/
  commerce/
  fulfilment/
  privacy/
lib/
  auth/
  db/
  storage/
  security/
  i18n/
  observability/
providers/
  anthropic/
  recraft/
  stripe/
  resend/
  inngest/
  analytics/
schemas/
emails/
pdf/
supabase/
  migrations/
tests/
  unit/
  integration/
  e2e/
docs/
  product/
  operations/
```

## 6. Runtime rules

- Use Node runtime for `sharp`, PDF production and vendor SDK compatibility unless a route is proven Edge-safe.
- AI work must not depend on an open browser request.
- Browser initiates a request that creates an idempotent job and receives a job/project status.
- Inngest processes the job, writes progress and outcome.
- UI polls conservatively or uses a verified real-time subscription without exposing private rows.
- Stripe webhook returns quickly after durable event handling/job dispatch.
- All mutations validate server-side.

## 7. Required API/use-case surface

Exact route shape may change, but capabilities must include:

```text
POST   /api/projects
GET    /api/projects/:id
PATCH  /api/projects/:id/session
POST   /api/projects/:id/uploads/presign
POST   /api/projects/:id/uploads/complete
POST   /api/projects/:id/meaning-map/generate
PATCH  /api/projects/:id/meaning-map
POST   /api/projects/:id/meaning-map/confirm
POST   /api/projects/:id/preview
POST   /api/projects/:id/checkout
POST   /api/stripe/webhook
POST   /api/projects/:id/variants
POST   /api/projects/:id/select
POST   /api/projects/:id/revisions
POST   /api/projects/:id/curator-note
POST   /api/projects/:id/approve
GET    /api/projects/:id/downloads
POST   /api/projects/:id/delete
GET    /api/reveal/:token
```

Admin use cases:

```text
GET    /api/admin/operations
GET    /api/admin/orders/:id
POST   /api/admin/orders/:id/preflight
POST   /api/admin/orders/:id/production-bundle
PATCH  /api/admin/orders/:id/fulfilment
POST   /api/admin/orders/:id/incident
POST   /api/admin/jobs/:id/retry
```

Do not expose a generic AI proxy endpoint.

## 8. Storage design

Private buckets:

- `source-photos`
- `generated-private`
- `final-deliverables`
- `production-bundles`

Rules:

- no bucket is public;
- object path starts with owner/project IDs that are validated server-side;
- original upload is quarantined until decoded, validated, EXIF-stripped and re-encoded;
- sanitised derivative becomes the approved AI input;
- untrusted SVG from provider is sanitised before storage or display;
- downloads use short-lived signed URLs or authenticated streaming;
- preview delivered from a separate watermarked derivative;
- source provider URLs are never persisted as customer-facing URLs.

## 9. Image production

### Aspect and crop

40 × 50 cm is a 4:5 ratio. Generation and preview should use 4:5 where supported. Preflight must protect important content from frame/crop loss.

### Raster

Do not promise that metadata DPI alone makes an image print-ready. Calculate effective resolution from actual pixel dimensions and physical size.

At 40 × 50 cm:

- preferred effective output: approximately 300 ppi where achievable;
- minimum allowed for launch must be agreed with the sampled print provider;
- upscaling method and original size recorded.

### Vector

- use native vector generation for Modern Essence;
- parse and sanitise SVG;
- reject scripts, external references, embedded remote fonts and event handlers;
- render a raster proof and compare dimensions;
- generate print PDF according to provider requirements.

### Colour

Default web and internal interchange is sRGB unless the selected print provider requires a documented profile. Never silently convert without a recorded production transform.

## 10. Watermarking

Watermark is applied server-side to a derivative:

- visible at typical screen size;
- difficult to crop without damaging composition;
- restrained enough to evaluate art;
- contains MEANINGFRAME wordmark and `Personal Preview`;
- original remains private;
- response headers discourage caching/indexing where appropriate.

## 11. Authentication and authorisation

- anonymous browser gets a signed, HttpOnly project session token;
- project access migrates to verified Supabase user after magic link;
- all project queries include ownership checks/RLS;
- admin role stored in protected profile/claims and rechecked server-side;
- do not rely on hidden UI for access control;
- sensitive actions require recent authentication where practical.

## 12. Payment architecture

- products/prices come from server allow-list;
- Stripe Checkout session includes project ID as validated metadata;
- webhook verifies signature on raw body;
- webhook event stored and deduplicated;
- order state transition occurs inside a transaction;
- paid event grants entitlements and dispatches jobs;
- browser success URL never grants purchase;
- refunds and disputes reconcile into local state.

## 13. Job architecture

Job types:

- `OBSERVE_PHOTOS`
- `GENERATE_MEANING_MAP`
- `GENERATE_PREVIEW`
- `GENERATE_PAID_VARIANTS`
- `GENERATE_REVISION`
- `GENERATE_CURATOR_NOTE`
- `FINALISE_DELIVERABLES`
- `BUILD_PRODUCTION_BUNDLE`
- `DELETE_PROJECT_DATA`
- `SEND_NOTIFICATION`

Each job:

- has unique idempotency key;
- records project and safe correlation ID;
- has bounded retries;
- classifies retryable/non-retryable failures;
- records provider cost/latency;
- never logs raw secret or full personal payload;
- updates visible progress;
- escalates repeated failure to admin.

## 14. Environment strategy

Environments:

- local;
- preview/staging;
- production.

Requirements:

- separate Supabase projects or safely isolated environment strategy;
- Stripe test keys only outside production;
- separate storage;
- no production customer content copied to local;
- production domain only after launch gate;
- environment validation at boot/build for required values.

## 15. CI/CD

Pull request checks:

- formatting;
- lint;
- typecheck;
- unit tests;
- integration tests;
- production build;
- JSON schema validation;
- migration lint;
- dependency audit;
- secret scan;
- Playwright smoke path on preview where secrets are safely configured.

Production deploy:

- protected branch or explicit approval;
- migration plan;
- rollback note;
- smoke test;
- release record with prompt/model/schema versions.

## 16. Technical cost controls

- configurable maximum dynamic follow-ups;
- one free preview entitlement;
- per-account/IP/device rate limits;
- token/output limits;
- prompt caching where safe and supported;
- image operation count caps;
- explicit retry caps;
- cost recorded per provider call;
- daily cost anomaly alert;
- kill switch for free preview generation without disabling paid delivery recovery.

## 17. Dependency rule

Every material external dependency must be recorded with:

- purpose;
- data sent;
- data region;
- retention/training terms;
- DPA status;
- current cost/free limit;
- failure fallback;
- owner;
- removal strategy.

Paid-plan activation requires founder approval.

