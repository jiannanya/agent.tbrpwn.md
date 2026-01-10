# TBR-PWN (Target–Behave–Remember + Plan–Work–Note)

This is an AI agent loop promote project.

- **Outer loop (TBR)**: keeps stable state on disk.
- **Inner loop (PWN)**: increases divergence + iteration inside each phase until the plan converges.

## Files

- `promote.tbrpwn.main.md` — entry point
- `agent.tbrpwn.impl.md` — detailed AI agent operating contract (Lite + Havy)
- `promote.tbrpwn.base.md` — generic operating contract
- `promote.tbrpwn.coding.md` — coding
- `promote.tbrpwn.debugging.md` — debugging
- `promote.tbrpwn.research.md` — research
- `promote.tbrpwn.product.md` — product delivery
- `promote.tbrpwn.automation.md` — workflow automation
- `.tbrpwn/tbr/` — outer loop runtime state files
- `.tbrpwn/pwn/` — inner loop runtime state files (Level1/2/3)
- `.tbrpwn/LOG.md` — per-cycle append-only log

Template/reference (do not edit during execution):

- `tbr/`
- `pwn/`

## Quick start

1. Choose one promote file (start with `promote.tbrpwn.main.md`).
2. User fills `.tbrpwn/tbr/TARGET.md` (init target).
3. For each request, triage first (Lite vs Havy), then run the corresponding cycle:
   - Lite: run `LiteCycle` (Level2 only) and update BEHAVE/REMEMBER (+ TARGET only if changed)
   - Havy: run a full `OuterCycle` (Level1 + Level2 + Level3)
4. After each completed cycle, append `.tbrpwn/LOG.md` (`LiteCycle.vN` or `OuterCycle.vN`).

Bootstrap:

- If `.tbrpwn/` is missing, recreate it from the templates (`tbr/` and `pwn/`) or restore from VCS.

## Stop condition

Stop only when:

- `.tbrpwn/tbr/TARGET.md` acceptance is complete, and
- a full outer cycle would not change `.tbrpwn/tbr/TARGET.md`.

## Anti-stall rule

If a PLAN is stable but WORK is not done, execute WORK and update NOTE; do not keep “planning”.

## Quality gates (hard rule)

- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Minimal walkthrough (one outer cycle)

- Level1 (Target): PLAN ← (TARGET, NOTE, WORK) → WORK/NOTE → execute WORK → NOTE → PLAN … until stable → merge to TARGET/BEHAVE/REMEMBER
- Level2 (Behave): same loop → merge to BEHAVE/REMEMBER
- Level3 (Remember): same loop → merge to REMEMBER
- Then rewrite TARGET from BEHAVE+REMEMBER and repeat if needed
