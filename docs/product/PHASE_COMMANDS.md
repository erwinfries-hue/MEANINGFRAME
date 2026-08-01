# MEANINGFRAME — COPY-PASTE PHASE COMMANDS

## First run

Use `CLAUDE_CODE_START_PROMPT.txt`.

## Approve Phase 1

```text
Read docs/product/ and all current docs/implementation/ records again.
I approve Phase 1 only.
Execute Phase 1 from docs/product/13_IMPLEMENTATION_PHASES.md.
Implement, test and verify all Phase 1 exit criteria, update every implementation record and stop with the required evidence report.
Do not begin Phase 2.
```

## Generic later phase

```text
Read docs/product/ and all current docs/implementation/ records again.
I approve Phase [N] only.
Execute Phase [N] from docs/product/13_IMPLEMENTATION_PHASES.md.
Resolve only issues within the approved phase or mandatory security/legal corrections.
Implement, test and verify all Phase [N] exit criteria, update every implementation record and stop with the required evidence report.
Do not begin Phase [N+1].
```

## Fix a failed phase

```text
Do not begin a new phase.
Review the last phase report and all failing evidence.
Fix only the unresolved requirements of Phase [N], rerun the relevant full verification set, update docs/implementation/ and issue a corrected Phase [N] evidence report.
Stop afterward.
```

## Prepare production launch

Use only after Phase 7 is fully approved:

```text
I approve Phase 8 controlled launch preparation only.
Read the complete product and implementation records.
Verify every launch gate with current evidence. Do not bypass missing legal identity, production credentials, print-sample approval, privacy deletion proof, Stripe separation, security findings or operational ownership.
Prepare production, run one controlled smoke transaction and stop before scaling any marketing.
Return the Phase 8 evidence report and exact founder actions.
```

