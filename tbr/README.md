# TBR (Target–Behave–Remember) File Set — for TBR-PWN

This folder is the stable outer-loop state.

## Files
- `TARGET.md` — goal/constraints/acceptance (source of truth)
- `BEHAVE.md` — next-step policy derived from TARGET
- `REMEMBER.md` — minimal durable memory

## How PWN fits
- Target phase runs Level1 PWN and then merges into TARGET/BEHAVE/REMEMBER.
- Behave phase runs Level2 PWN and then merges into BEHAVE/REMEMBER.
- Remember phase runs Level3 PWN and then merges into REMEMBER.

## Discipline
- Keep each file short.
- Evidence beats description.
- One outer cycle should produce either: checked acceptance or new objective evidence.
- Each outer cycle must record Gate check results (PASS/FAIL + evidence pointers) inside TARGET/BEHAVE/REMEMBER.

## Quality gates
- TARGET must satisfy the quality gate in `TARGET.md` (checkable acceptance + evidence expectations).
- BEHAVE must satisfy the quality gate in `BEHAVE.md` (one-step + objective verification + rollback).
- REMEMBER must satisfy the quality gate in `REMEMBER.md` (evidence pointers, minimality, no transcripts).

Hard rule:
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.
