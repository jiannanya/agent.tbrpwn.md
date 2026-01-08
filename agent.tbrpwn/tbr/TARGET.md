# TARGET.md

## TARGET.v1

### Goal
<one sentence>

### Constraints
- <platform>
- <performance>
- <security/policy>

### Non-goals
- <explicitly not doing>

### Acceptance (Definition of Done)
- [ ] <criterion 1> — evidence: <file/command output>
- [ ] <criterion 2> — evidence: <file/command output>
- [ ] <criterion 3> — evidence: <file/command output>

### Open questions (only blocking)
- <question 1>

### Gate check result (this outer cycle)
- Result: <PASS|FAIL>
- Checked against: <TARGET.vN>
- Evidence pointers:
	- <at least 1 file path / command output; if none, Result must be FAIL>
- Notes (if FAIL, list what is missing):
	- <missing gate item>

---

## Update rule
- Only mark acceptance items when evidence exists.
- If a checkbox grows, split it.
- After each full outer cycle, rewrite TARGET using current `.tbrpwn/tbr/BEHAVE.md` + `.tbrpwn/tbr/REMEMBER.md`.

## Quality gate (objective)
TARGET is acceptable only if all are true:
- [ ] Goal is one sentence and unambiguous
- [ ] Constraints are explicit and testable (not vibes)
- [ ] Non-goals are explicit (what we will NOT do)
- [ ] Every acceptance item is checkable and names expected evidence
- [ ] Open questions contains only blocking questions

Anti-patterns:
- “Acceptance: implement X” (not checkable)
- Acceptance items with no evidence expectation
- Hidden requirements only mentioned in NOTE
