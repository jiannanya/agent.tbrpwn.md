# PWN (Plan–Work–Note) inner loop

PWN runs inside a single TBR phase to increase iteration capacity.

Note:
- The runtime state must be updated under `.tbrpwn/pwn/`.
- The repo-root `pwn/` folder is template/reference.

## Files per level
- `PLAN.md` — evolving plan; plan stabilizes → level ends
- `WORK.md` — executable actions/artifacts
- `NOTE.md` — exploration, measurements, alternatives, questions

## Versioning convention (required)
- Maintain `PLAN.vN`, `WORK.vN`, `NOTE.vN` sections.
- Every new version must include a short **Delta since v(N-1)**.
- Use the “Meaningful PLAN change” rule to decide whether PLAN truly changed.

## PWN loop (repeat)
1) PLAN ← (current TBR state + NOTE + WORK)
2) WORK/NOTE ← PLAN
3) Execute WORK; append objective outputs to NOTE
4) PLAN ← (WORK results + NOTE)
5) Stop when PLAN is stable

## Meaningful PLAN change
A PLAN update is meaningful only if it changes:
- task set (add/remove/merge/split)
- ordering/dependencies
- success criteria / verification
- rollback/safety constraints

Pure rewording is not meaningful.

## Anti-stall rule
If PLAN is stable but WORK isn’t done, execute WORK and update NOTE.

## Merge
When a level ends, merge durable decisions and evidence into TBR.

## Per-cycle log
- After completing Level1+Level2+Level3 and merging, append `.tbrpwn/LOG.md`.

Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.
