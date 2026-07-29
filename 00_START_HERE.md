# MEANINGFRAME — START HERE

Version: 1.0  
Date: 29 July 2026  
Owner: AXIA4 Digital  
Status: Authoritative product package for the controlled MVP

## 1. What this package is

This package is the single source of truth for building the first productive MEANINGFRAME MVP with Claude Code.

MEANINGFRAME is not a generic AI image generator. It is a guided co-creation service that turns what makes a person meaningful into a personal work of art, a curatorial interpretation and, optionally, a finished physical gift.

Brand line:

> MEANINGFRAME  
> WHAT MATTERS, BECOMES ART.  
> by AXIA4 Digital

## 2. The required working method

Claude Code must:

1. read every file in this package completely;
2. treat `DECISION_REGISTER.md` as binding;
3. identify contradictions before writing feature code;
4. execute only the currently approved implementation phase;
5. never silently expand the MVP;
6. never add a paid vendor or material recurring cost without approval;
7. implement real, testable flows rather than mock buttons or TODO placeholders;
8. prove every phase with tests and a short evidence report;
9. preserve privacy, deletion and consent requirements as release blockers;
10. keep all external AI, payment, email and fulfilment integrations behind typed adapters.

## 3. First Claude Code instruction

Create or open an empty Git repository for the application. Place this complete folder at:

`docs/product/`

Then paste the exact contents of `CLAUDE_CODE_START_PROMPT.txt` into Claude Code.

Claude Code must initially execute **Phase 0 only**. Phase 0 is an inspection and implementation-planning gate. It must not build product features yet.

## 4. Authority order

If instructions conflict, use this priority:

1. `DECISION_REGISTER.md`
2. `04_MVP_SCOPE_AND_ROADMAP.md`
3. `06_FUNCTIONAL_REQUIREMENTS_AND_ACCEPTANCE.md`
4. `10_PRIVACY_SECURITY_LEGAL.md`
5. `13_IMPLEMENTATION_PHASES.md`
6. all remaining package documents

Claude Code must document any unresolved conflict in `docs/product/OPEN_QUESTIONS.md` and stop only if it prevents a safe implementation.

## 5. Definition of a productive MVP

The MVP is productive only when a real customer can:

1. understand the offer;
2. begin without creating a password;
3. complete a guided Co-Author Session;
4. confirm a structured Meaning Map;
5. receive one protected personalised preview;
6. buy a Digital or Signature Edition through Stripe;
7. receive three refined variants;
8. choose one and request one guided revision;
9. approve and download the final artwork and Curator’s Note;
10. place a physical order that staff can fulfil through the admin workflow;
11. exercise privacy and deletion rights.

Admin staff must be able to review orders, download a validated production bundle, update fulfilment status and trigger customer notifications.

## 6. What is deliberately not included

The MVP does not include:

- a public prompt box;
- unlimited generations;
- arbitrary named artist imitation;
- cartoons, memes or novelty filters;
- company and team artwork;
- an open art marketplace;
- multiple print providers;
- automated print-on-demand API fulfilment;
- subscriptions;
- native mobile apps;
- social feeds;
- public galleries without explicit opt-in;
- crypto, NFT or blockchain functionality.

## 7. Package map

| File | Purpose |
|---|---|
| `DECISION_REGISTER.md` | Binding founder decisions |
| `01_EXECUTIVE_PRODUCT_BRIEF.md` | Product thesis and customer value |
| `02_MARKET_POSITIONING_BUSINESS_MODEL.md` | Market logic, competition and economics |
| `03_BRAND_CONTENT_DESIGN_SYSTEM.md` | Brand, UI direction and copy |
| `04_MVP_SCOPE_AND_ROADMAP.md` | In scope, out of scope and evolution |
| `05_UX_USER_FLOWS_AND_COPY.md` | Detailed customer and admin journeys |
| `06_FUNCTIONAL_REQUIREMENTS_AND_ACCEPTANCE.md` | Testable functional requirements |
| `07_AI_ORCHESTRATION_AND_PROMPTS.md` | AI pipeline, schemas and production prompts |
| `08_TECHNICAL_ARCHITECTURE.md` | Stack, boundaries and integrations |
| `09_DATA_MODEL_AND_STATE_MACHINES.md` | Entities, lifecycle and state transitions |
| `10_PRIVACY_SECURITY_LEGAL.md` | Privacy, safety and compliance requirements |
| `11_COMMERCE_FULFILLMENT_OPERATIONS.md` | Stripe, products and manual fulfilment |
| `12_ANALYTICS_VALIDATION_AND_QA.md` | Metrics, experiments, QA and launch gates |
| `13_IMPLEMENTATION_PHASES.md` | Controlled phase-by-phase build plan |
| `14_CLAUDE_CODE_MASTER_PROMPT.md` | Persistent implementation instruction |
| `15_REFERENCE_EXAMPLE.md` | Fictional end-to-end quality benchmark |
| `schemas/` | Machine-readable output contracts |
