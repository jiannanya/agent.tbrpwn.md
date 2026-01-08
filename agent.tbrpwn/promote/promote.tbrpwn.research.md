# promote.tbrpwn.research.md — TBR-PWN (Research)

## Target (fill first)
**TARGET.v1**
- Research question:
- Deliverable: memo | experiment plan | prototype
- Constraints: time/compute/data
- Acceptance:
  - [ ] Problem formulation
  - [ ] Baseline defined
  - [ ] Proposed method + tradeoffs
  - [ ] Evaluation plan
  - [ ] Risks/limitations

## Behave (derive each iteration)
**BEHAVE.vN**
- Step (one step only): write section | define baseline | design experiment | analyze results
- Verification: internal consistency check; metric definitions; reproducibility notes

## Remember (persist minimal state)
**REMEMBER.vN**
- Current assumptions:
- Key definitions/metrics:
- Decisions + rationale:
- Open questions:

---

## TBR-PWN research rules
- Level1 turns the question into checkboxes + a baseline.
- Level2 WORK must produce either a memo section or an experiment artifact.
- NOTE can include negative results; Level3 decides what is durable and keeps it minimal.

## Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Runtime location
- Write execution updates under `.tbrpwn/tbr/` and `.tbrpwn/pwn/`.
- Append `.tbrpwn/LOG.md` after each full outer cycle.

## Target update policy
- Turn vague goals into checkboxes.
- When evidence contradicts assumptions, update assumptions explicitly.
