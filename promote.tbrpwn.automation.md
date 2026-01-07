# promote.tbrpwn.automation.md — TBR-PWN (Workflow Automation)

## Target (fill first)
**TARGET.v1**
- Workflow goal:
- Systems/tools:
- Side effects:
- Permissions:
- Acceptance:
  - [ ] Steps defined with inputs/outputs
  - [ ] Idempotency/dedupe defined
  - [ ] Error handling + retry policy
  - [ ] Execution verified
  - [ ] Audit evidence recorded

## Behave (derive each iteration)
**BEHAVE.vN**
- Step (one step only): design | implement | run | verify
- Idempotency key / dedupe strategy:
- Rollback / compensating action:
- Verification evidence:

## Remember (persist minimal state)
**REMEMBER.vN**
- External IDs (tickets, runs, deployments):
- Last execution timestamp:
- Dedupe keys used:
- Evidence excerpts:

---

## TBR-PWN automation rules
- Level1 NOTE must capture: systems, permissions, side effects, and unknowns.
- Level2 WORK must be idempotent-by-default (explicit “already done” checks).
- Level2 NOTE must record: external IDs, dedupe keys, and irreversible actions.
- Level3 must compress REMEMBER to an audit trail (IDs + evidence pointers).

## Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Target update policy
- If a step has side effects, require evidence and IDs before moving on.
- Stop before duplicates: if uncertain, ask user.
