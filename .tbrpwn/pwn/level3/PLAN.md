# Level3 PLAN.md — Remember phase PWN (runtime)

## PLAN.v1

### Delta since previous version
- N/A (initial)

### Purpose
Improve REMEMBER quality: correctness, minimality, and usefulness.

### Inputs
- `.tbrpwn/tbr/REMEMBER.md`
- `.tbrpwn/pwn/level3/NOTE.md`
- `.tbrpwn/pwn/level3/WORK.md`

### Plan (ordered)
1. Delete stale items and compress
2. Replace claims with evidence pointers
3. Keep only facts/decisions/evidence/blockers/risks

### Stop condition
Stop Level3 when PLAN is stable (no meaningful delta across 2 versions).

### Meaningful change rule
PLAN changes are meaningful only if they change task set, ordering, success criteria, or safety/rollback (when applicable).

### Plan stability checklist (required to stop)
Before declaring the PLAN stable, confirm all are true:
- [ ] Task set unchanged vs previous PLAN
- [ ] Ordering/dependencies unchanged vs previous PLAN
- [ ] Success criteria / verification unchanged vs previous PLAN (if applicable)
- [ ] Rollback/safety constraints unchanged vs previous PLAN (if applicable)

If any box is unchecked, the PLAN is not stable.

### Merge output (when stable)
Merge to:
- `.tbrpwn/tbr/REMEMBER.md`
