# MEANINGFRAME — PRIVACY, SECURITY & LEGAL REQUIREMENTS

## 1. Status

This document defines product and engineering requirements. It is not a substitute for final legal review before public launch.

The Swiss pilot must be designed for:

- Swiss Federal Act on Data Protection;
- GDPR readiness for later DACH activation;
- EU AI Act transparency obligations relevant from 2 August 2026;
- Swiss and later EU consumer-commerce requirements;
- image, personality, copyright and contractual rights.

Reference starting points:

- Swiss FDPIC: https://www.edoeb.admin.ch/en
- EU AI transparency: https://digital-strategy.ec.europa.eu/en/policies/guidelines-transparency-ai-generated-content
- EU consumer rights: https://eur-lex.europa.eu/EN/legal-content/summary/consumer-information-right-of-withdrawal-and-other-consumer-rights.html

## 2. Privacy posture

Public promise:

> Your memories are used to create your project, not to train AI. Source photos and personal project inputs are automatically deleted.

Engineering implications:

- data minimisation;
- purpose limitation;
- documented retention;
- private storage;
- vendor contracts/data terms;
- user controls;
- no hidden training consent;
- no public portfolio by default;
- no sale or advertising use of personal project data.

## 3. Data categories

### Account

- email;
- preferred language;
- minimal display name.

### Creative project

- subject nickname/display name;
- relationship;
- occasion;
- traits, memories, places and values supplied by Co-Author;
- photos;
- visual preferences and exclusions;
- generated Meaning Map and outputs.

### Commerce

- Stripe/customer/order references;
- edition and frame choice;
- delivery name/address for Signature order;
- fulfilment/tracking;
- price, tax and refund.

### Operations

- consent records;
- job metadata;
- security/audit events;
- support and incident records.

Never collect card numbers directly.

## 4. Legal-basis mapping for counsel validation

Candidate mapping:

- account and project delivery: contract/performance steps;
- photo and story processing: contract plus explicit confirmation of permission; assess consent needs by context;
- marketing email: separate opt-in;
- security logs: legitimate interest/legal security;
- accounting records: legal obligation;
- optional public showcase: separate, revocable explicit consent.

Do not bundle marketing/publication consent into purchase.

## 5. Photos and third-person data

The subject is often not the buyer. Required safeguards:

- Co-Author must confirm a right or permission to use uploaded photos for a private artwork;
- terms prohibit harassment, deception and non-consensual intimate content;
- product is private by default;
- no public sharing by MEANINGFRAME without separate consent;
- purchaser must be 18+;
- if subject is a minor, require guardian confirmation from the Co-Author and apply stricter content rules;
- do not perform face recognition, identity verification or biometric identification;
- photo observation must avoid sensitive inference.

## 6. Vendor processing

Before production:

1. record every processor/subprocessor;
2. verify data-processing terms and DPA availability;
3. verify whether API content is used for training;
4. verify retention and deletion options;
5. verify data location and cross-border safeguards;
6. configure no-training/lowest-retention enterprise or API settings where available;
7. disclose material vendors/categories in privacy policy;
8. send only minimised data.

Do not upload postal addresses to AI providers.

## 7. Consent and notices

Required separate records:

- Terms acceptance;
- Privacy notice acknowledgement;
- permission to use uploaded photos;
- acknowledgement that generative AI processes supplied material;
- guardian confirmation for minor subject;
- final approval for production;
- optional marketing;
- optional public showcase.

Each record stores policy version and timestamp. Never pre-check optional consent.

## 8. AI transparency

Customer-facing requirements:

- disclose AI co-creation before session submission and again in final deliverables;
- mark generated/manipulated content in a machine-readable way where required and technically supported;
- include a visible co-creation disclosure in Certificate and Reveal Page;
- do not pretend the Curator’s Note was written by an independent human critic;
- do not claim a human artist painted the work;
- disclose Atelier Review as human review only when it actually occurred.

Implement AI metadata/marking in a provider-agnostic service so requirements can evolve.

## 9. Intellectual property and personality rights

### Customer inputs

Terms should state that the Co-Author:

- retains rights in material they own;
- grants MEANINGFRAME a limited licence to process it for the project;
- confirms necessary permission for third-party material;
- must not upload infringing or unlawful content.

### Generated outputs

Do not guarantee copyright protection or exclusivity beyond the service’s one-project composition promise. Legal treatment of AI-generated work can vary.

Commercial model for MVP:

- customer receives a personal-use licence to paid final outputs;
- MEANINGFRAME may retain only as required by retention/operations;
- no portfolio, resale or model training without separate agreement;
- commercial-use licence is post-MVP.

### Artist and brand references

- no direct imitation of a named living or deceased artist;
- no copyrighted character, trademark or brand as the central design;
- provide generic aesthetic alternatives;
- moderation and prompt filters apply before provider call.

## 10. Consumer terms

Terms and checkout must clearly describe:

- digital/physical contents;
- prices and included Swiss standard delivery;
- generation and approval process;
- one included revision;
- additional revision price;
- approximate production timing as an estimate;
- personalised nature of goods;
- cancellation/refund rules;
- quality-failure remedies;
- personal-use licence;
- privacy retention;
- AI assistance.

For future EU/DACH activation, implement but do not activate without counsel:

- 14-day withdrawal information;
- exception for goods made to consumer specification/clearly personalised;
- explicit consent and acknowledgement before immediate digital performance where required;
- VAT and local business disclosures.

## 11. Refund and quality policy

Recommended MVP policy:

- free preview carries no purchase obligation;
- after paid generation begins, ordinary change-of-mind handling follows applicable personalised digital-service terms;
- technical corruption, missing paid deliverable or material departure caused by system failure is corrected without consuming the included revision;
- physical damage or print defect qualifies for reprint or appropriate remedy;
- dislike alone after explicit final print approval is not automatically a production defect;
- staff retains discretion for goodwill during controlled beta.

Final wording requires counsel review.

## 12. Security controls

### Accounts

- passwordless magic link;
- short link expiry;
- rate-limited send/resend;
- session rotation;
- secure cookies;
- recent authentication for deletion.

### Application

- server-side authorisation;
- RLS;
- validated mutations;
- CSP;
- HSTS on production;
- secure headers;
- CSRF-safe patterns;
- dependency/secret scanning;
- admin role separation;
- audit of privileged actions.

### Uploads

- allow-listed image types;
- actual decode and re-encode;
- EXIF stripping;
- pixel and byte limits;
- malware/image-bomb safeguards;
- private quarantine;
- random object names;
- sanitised SVG.

### Payments

- Stripe-hosted PCI-safe components;
- raw-body webhook verification;
- event idempotency;
- no card data in local DB/logs.

### Secrets

- only platform secret stores;
- never committed;
- least privilege;
- rotation runbook;
- separate test/production.

## 13. Logging and support

Logs must not contain:

- photos or signed URLs;
- full project answers;
- email/address unless strictly required and redacted;
- tokens or secrets;
- Stripe payloads beyond minimised identifiers;
- raw AI prompts.

Support admin views show the minimum required information. Access to raw photos must be exceptional, role-restricted and audited.

## 14. Retention

Binding:

- abandoned unpurchased creative inputs: seven days after last activity;
- purchased raw photos/free text/observations: 30 days after completion;
- paid final deliverables: 12 months;
- reveal links expire or revoke with final retention/deletion;
- financial records: legal/accounting duration, separated and minimised.

Retention countdown must be visible in the customer project.

## 15. Rights workflow

Customer actions:

- download core project data;
- delete creative project now;
- revoke Reveal Page;
- opt out of marketing;
- contact privacy support.

Operations:

- verify requester;
- create tracked request;
- execute across DB/storage/vendors under platform control;
- preserve only required legal record;
- confirm completion;
- document exceptions.

## 16. Incident response

Before launch, create:

- severity levels;
- incident owner;
- containment checklist;
- credential rotation steps;
- provider contact list;
- affected-data assessment;
- notification decision process;
- customer/regulator communication template;
- post-incident review.

Release blocker: no known critical vulnerability or exposed personal bucket.

## 17. Required legal pages

- Imprint/legal notice with AXIA4 entity details once available;
- Terms of Service;
- Privacy Policy;
- Cookie/analytics notice;
- AI Co-Creation Disclosure;
- Refund and Quality Policy;
- contact/support information.

Use placeholders only in non-production. Production deployment must fail or visibly block checkout if mandatory business identity fields are not configured.

