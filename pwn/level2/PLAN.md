# Level2 PLAN.md — Behave phase PWN

## PLAN.v1

### Delta since previous version
- N/A (initial)

### Purpose
Iteratively improve BEHAVE and REMEMBER so the next execution step is minimal, safe, and verifiable.

### Inputs
- `tbr/TARGET.md`
- `tbr/BEHAVE.md`
- `tbr/REMEMBER.md`
- `pwn/level2/NOTE.md`
- `pwn/level2/WORK.md`

### Plan (ordered)
1. Ensure BEHAVE is the smallest step toward TARGET
2. Define exact verification and pass signal
3. Execute one step (or a smaller sub-step)
4. Record evidence and decisions

### Stop condition
Stop Level2 when PLAN is stable (no meaningful delta across 2 versions).

### Meaningful change rule
PLAN changes are meaningful only if they change task set, ordering, success criteria, or safety/rollback.

### Plan stability checklist (required to stop)
Before declaring the PLAN stable, confirm all are true:
- [ ] Task set unchanged vs previous PLAN
- [ ] Ordering/dependencies unchanged vs previous PLAN
- [ ] Success criteria / verification unchanged vs previous PLAN
- [ ] Rollback/safety constraints unchanged vs previous PLAN

If any box is unchecked, the PLAN is not stable.

### Merge output (when stable)
Merge to:
- `tbr/BEHAVE.md`
- `tbr/REMEMBER.md`
