# MEANINGFRAME — OPEN QUESTIONS

Version: 1.0
Created: 2026-08-01
Status: Tracks unresolved items identified while reviewing the product package before Phase 0. Per `00_START_HERE.md` §4, this register does not override `DECISION_REGISTER.md`; it lists what is not yet decided.

Each item is resolved by founder answer and then either promoted into `DECISION_REGISTER.md` (if binding and durable) or into `docs/implementation/` records (if operational/technical).

## Status legend

- `OPEN` — no founder answer yet
- `ANSWERED` — resolved, decision recorded below with date
- `DEFERRED` — explicitly postponed to a later phase per the package's own gating rules

## 1. Business and legal readiness

| ID | Question | Status |
|---|---|---|
| Q-001 | Are `meaningframe.com` / `.ch` / `.de` already registered? If yes, where, and is DNS available to point at Vercel? | OPEN |
| Q-002 | What is the AXIA4 legal entity name, address and VAT/commercial-register status to put in Terms/Privacy/Imprint (even as controlled placeholders pre-launch)? | OPEN |
| Q-003 | Are `hello@`, `support@` and `privacy@meaningframe.com` mailboxes set up yet? | OPEN |
| Q-004 | Which accounts already exist vs. still need creating: GitHub (repo exists), Vercel, Supabase, Stripe, Anthropic API, Recraft API, Resend, Inngest? | OPEN |
| Q-005 | Who is the operational owner for: customer support, Signature fulfilment/print submission, and Atelier Review (human reviewer) — or is Atelier Review disabled at launch? | OPEN |
| Q-006 | Swiss VAT/tax treatment for digital + physical goods — confirmed by accountant, or still to be obtained? | OPEN |

## 2. Physical product / print provider

| ID | Question | Status |
|---|---|---|
| Q-007 | Gelato, Prodigi or another candidate as primary Swiss print provider — or proceed to Phase 0 with both shortlisted and decide after samples (per `11_COMMERCE_FULFILLMENT_OPERATIONS.md` §5)? | OPEN |
| Q-008 | Has any print sample already been ordered/evaluated, or does that happen during/after Phase 6? | DEFERRED — package assigns this to the Phase 6 gate; only relevant now if founder wants to start it in parallel |

## 3. Product-content depth (below binding-decision level)

These are areas where `DECISION_REGISTER.md` fixes the direction but the package intentionally leaves exact content for Phase 2/3 implementation (per `05_UX_USER_FLOWS_AND_COPY.md`, trait/question lists are marked "suggested", not final).

| ID | Question | Status |
|---|---|---|
| Q-009 | Is the "suggested" DE trait-chip list in `05_UX_USER_FLOWS_AND_COPY.md` §Stage B final, or does the founder want to edit/extend it before Phase 2? | DEFERRED — Phase 2 scope |
| Q-010 | Any additional occasions beyond the four "initial occasions" (D-026) planned for MVP launch copy, or exactly those four? | OPEN |

## 4. Budget and timeline confirmation

| ID | Question | Status |
|---|---|---|
| Q-011 | Confirm the CHF 7,500–10,000 / 8–10 week frame (D-034) is still current, and whether a start date is fixed. | OPEN |

## Resolution log

### 2026-08-01 — Q-001, Q-003, Q-004

Founder confirmed: none of domain registration, AXIA4 legal-entity documentation, or technical vendor accounts (Vercel, Supabase, Stripe, Anthropic, Recraft, Resend, Inngest) exist yet. GitHub repository is the only asset currently in place.

This does not block Phase 0. Per `FOUNDER_HANDOFF.md` §2, accounts are created progressively; Phase 0's job is to produce the exact timing/order for each. Domain (Q-001) and legal entity (Q-002) are required before Phase 8 (production launch) at the latest, and legal entity details are needed earlier for placeholder Terms/Privacy/Imprint copy in Phase 1/7. Status: OPEN, not currently blocking, revisit before Phase 1 exit and again before Phase 7.
