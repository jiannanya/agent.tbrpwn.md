# promote.tbrpwn.debugging.md — TBR-PWN (Debugging)

## Target (fill first)
**TARGET.v1**
- Symptom:
- Expected behavior:
- Repro steps:
- Environment:
- Acceptance:
  - [ ] Reproduced (or reason why not)
  - [ ] Root cause identified
  - [ ] Fix implemented
  - [ ] Verified / regression prevented

## Behave (derive each iteration)
**BEHAVE.vN**
- Step (one step only): reproduce | isolate | fix | verify
- Hypothesis (if isolating):
- Experiment + expected signal:
- Verification evidence to collect:

## Remember (persist minimal state)
**REMEMBER.vN**
- Exact error signature/log snippet:
- What was tried + outcome:
- Confirmed root cause (if known):
- Fix approach chosen (and why):

---

## TBR-PWN debugging rules
- Level1 must lock a reliable repro + environment description.
- Level2 PLAN must list hypotheses + experiments with expected signals.
- Level2 WORK must do one experiment/fix at a time; NOTE records exact outputs.
- Level3 compresses REMEMBER to the minimal reproducible story + evidence.

## Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Runtime location
- Write execution updates under `.tbrpwn/tbr/` and `.tbrpwn/pwn/`.
- Always triage first (Lite vs Havy) and then run either `LiteCycle` or `OuterCycle` as defined in `agent.tbrpwn.impl.md`.
- Append `.tbrpwn/LOG.md` after each completed cycle (`LiteCycle.vN` or `OuterCycle.vN`).

## Target update policy
- If reproduction becomes reliable, lock the repro steps.
- If root cause unclear after iterations, shrink the hypothesis scope.
- If fix is in, require evidence (re-run repro + tests) before marking done.
