# REMEMBER.md

## REMEMBER.v1

### Confirmed facts (with evidence pointers)
- <fact> — evidence: <file/tool output>

### Decisions (and why)
- <decision> — because <reason>

### Evidence (minimal excerpts)
- <test/build/run output snippet>

### Current status
- Last verification: PASS / FAIL
- Current blocker: <none | describe>

### Risks/limitations
- <risk>

### Gate check result (this outer cycle)
- Result: <PASS|FAIL>
- Checked against: <REMEMBER.vN>
- Evidence pointers:
	- <at least 1 file path / command output; if none, Result must be FAIL>
- Notes (if FAIL, list what is missing):
	- <missing gate item>

---

## Update rule
- Keep only durable signal: facts, decisions, evidence pointers, blockers, risks.
- Delete scratch exploration once it is merged (or proven irrelevant).

## Quality gate (objective)
REMEMBER is acceptable only if all are true:
- [ ] Every non-trivial claim has an evidence pointer (file path or command output)
- [ ] Decisions include a short “why”
- [ ] No long transcripts (prefer pointers or 1–3 line excerpts)
- [ ] No duplicate/stale items (delete or merge)
- [ ] Current status is up-to-date (PASS/FAIL + blocker)

Size guideline:
- Prefer keeping REMEMBER under ~60 lines; if it grows, compress aggressively.

Forbidden content:
- Raw chat logs
- Unverified assumptions stated as facts
- TODO lists that belong in TARGET acceptance
