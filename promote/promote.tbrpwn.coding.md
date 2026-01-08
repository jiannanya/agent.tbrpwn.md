# promote.tbrpwn.coding.md — TBR-PWN (Coding)

## Target (fill first)
**TARGET.v1**
- Feature/fix goal:
- Repo constraints (language/framework/OS):
- Acceptance:
  - [ ]
  - [ ]
- Non-goals:
  -

## Behave (derive each iteration)
**BEHAVE.vN**
- Step (one step only): <edit/search/test>
- Files to touch: <paths>
- Verification (fast → slow): <lint/typecheck/unit/build/run>
- Rollback: <revert strategy>
- Safety: no unrelated refactors; no invented results; no destructive ops.

## Remember (persist minimal state)
**REMEMBER.vN**
- Changed files summary:
- Current failing/passing checks:
- Key error signatures (if any):
- Decisions/assumptions:

---

## TBR-PWN coding rules
- Level1: establish build/test commands and acceptance criteria.
- Level2: each WORK item must produce code changes + verification outputs.
- Level3: compress REMEMBER to: facts, decisions, evidence pointers, blockers.

## Loop rules
- Each outer cycle must either close a checkbox or produce new verification evidence.
- Prefer tiny patches.
- If verification fails 3 times on the same step, shrink the target or ask the user.

## Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Runtime location
- Write execution updates under `.tbrpwn/tbr/` and `.tbrpwn/pwn/`.
- Append `.tbrpwn/LOG.md` after each full outer cycle.

## Target update policy
- Mark acceptance items only with evidence.
- Split scope instead of inflating a checkbox.
