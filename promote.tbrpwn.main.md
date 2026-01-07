# promote.tbrpwn.main.md — TBR-PWN (Entry Point)

Optional (more detailed):
- `agent.tbrpwn.md` — detailed AI agent operating contract (TBR-PWN)

## Pick ONE type-specific promote
- Generic: `promote.tbrpwn.base.md`
- Coding: `promote.tbrpwn.coding.md`
- Debugging: `promote.tbrpwn.debugging.md`
- Research: `promote.tbrpwn.research.md`
- Product: `promote.tbrpwn.product.md`
- Automation: `promote.tbrpwn.automation.md`

## Use the file-driven workspace
Outer loop state (source of truth):
- `tbr/TARGET.md`
- `tbr/BEHAVE.md`
- `tbr/REMEMBER.md`

Inner loop state (phase-local iteration):
- `pwn/level1/{PLAN,WORK,NOTE}.md` — Target phase
- `pwn/level2/{PLAN,WORK,NOTE}.md` — Behave phase
- `pwn/level3/{PLAN,WORK,NOTE}.md` — Remember phase

## Operating rule (outer cycle)
1) Target phase: run Level1 PWN until PLAN stabilizes → merge to TARGET/BEHAVE/REMEMBER
2) Behave phase: run Level2 PWN until PLAN stabilizes → merge to BEHAVE/REMEMBER
3) Remember phase: run Level3 PWN until PLAN stabilizes → merge to REMEMBER
4) Derive next TARGET from BEHAVE+REMEMBER → repeat

Stop only when TARGET acceptance is complete and TARGET no longer changes after an entire outer cycle.

Hard rule (quality gates):
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.
