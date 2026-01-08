# BEHAVE.md

## BEHAVE.v1

### Next step (one step only)
- <what to do next>

### What to touch
- Files/artifacts: <paths>

### Verify (objective)
- Command/check: <cmd or method>
- Pass signal: <what proves success>

### Rollback
- <how to undo>

### Safety rules
- Do not invent results.
- Keep changes minimal and reversible.
- If risky, shrink the step or ask the user.

### Gate check result (this outer cycle)
- Result: <PASS|FAIL>
- Checked against: <BEHAVE.vN>
- Evidence pointers:
  - <at least 1 file path / command output; if none, Result must be FAIL>
- Notes (if FAIL, list what is missing):
  - <missing gate item>

---

## Update rule
- BEHAVE must always remain “one smallest step only”.
- If more than one step is needed, split into the next smallest step and move the rest into TARGET acceptance items.

## Quality gate (objective)
BEHAVE is acceptable only if all are true:
- [ ] Exactly one step is described (no multi-step plans)
- [ ] “What to touch” lists concrete artifacts/files
- [ ] Verify includes an objective pass signal
- [ ] Rollback is feasible and explicit
- [ ] Safety rules include “no invented results”

Anti-patterns:
- Steps like “finish the feature” (too large)
- Verification like “looks good” (not objective)
