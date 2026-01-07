# TBR-PWN (Target–Behave–Remember + Plan–Work–Note)

This is an AI agent loop promote project.

- **Outer loop (TBR)**: keeps stable state on disk.
- **Inner loop (PWN)**: increases divergence + iteration inside each phase until the plan converges.

## Files
- `promote.tbrpwn.main.md` — entry point
- `agent.tbrpwn.md` — detailed AI agent operating contract (TBR-PWN)
- `promote.tbrpwn.base.md` — generic operating contract
- `promote.tbrpwn.coding.md` — coding
- `promote.tbrpwn.debugging.md` — debugging
- `promote.tbrpwn.research.md` — research
- `promote.tbrpwn.product.md` — product delivery
- `promote.tbrpwn.automation.md` — workflow automation
- `tbr/` — outer loop state files
- `pwn/` — inner loop state files (Level1/2/3)

## Quick start
1. Choose one promote file (start with `promote.tbrpwn.main.md`).
2. User fills `tbr/TARGET.md` (init target).
3. Run outer cycles until done:
   - Target phase → Level1 PWN → merge to T/B/R
   - Behave phase → Level2 PWN → merge to B/R
   - Remember phase → Level3 PWN → merge to R
   - Derive next TARGET from current BEHAVE+REMEMBER

## Stop condition
Stop only when:
- `tbr/TARGET.md` acceptance is complete, and
- a full outer cycle would not change `tbr/TARGET.md`.

## Anti-stall rule
If a PLAN is stable but WORK is not done, execute WORK and update NOTE; do not keep “planning”.

## Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Minimal walkthrough (one outer cycle)
- Level1 (Target): PLAN ← (TARGET, NOTE, WORK) → WORK/NOTE → execute WORK → NOTE → PLAN … until stable → merge to TARGET/BEHAVE/REMEMBER
- Level2 (Behave): same loop → merge to BEHAVE/REMEMBER
- Level3 (Remember): same loop → merge to REMEMBER
- Then rewrite TARGET from BEHAVE+REMEMBER and repeat if needed
