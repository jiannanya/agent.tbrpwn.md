# Level1 PLAN.md — Target phase PWN

## PLAN.v1

### Delta since previous version
- N/A (initial)

### Purpose
Refine TARGET/BEHAVE/REMEMBER so execution can start.

### Inputs
- `tbr/TARGET.md`
- `pwn/level1/NOTE.md`
- `pwn/level1/WORK.md`

### Plan (ordered)
1. Clarify Goal/Constraints/Acceptance/Non-goals
2. Draft BEHAVE: one smallest step + verify + rollback + safety
3. Seed REMEMBER: facts/assumptions/unknowns + evidence plan
4. Identify blocking questions

### Success criteria
- TARGET acceptance is checkable.
- BEHAVE has exactly one actionable step and objective verification.
- REMEMBER contains only durable signal.

### Stop condition
Stop Level1 when PLAN is stable (no meaningful delta across 2 versions).

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
- `tbr/TARGET.md`
- `tbr/BEHAVE.md`
- `tbr/REMEMBER.md`
