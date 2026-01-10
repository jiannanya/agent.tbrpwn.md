# LOG.md — TBR-PWN Execution Log (append-only)

This is an append-only log.

Rules:

- Append a `RequestTriage.vN` entry at the start of each user request.
- If triage decides Lite, append a `LiteCycle.vN` entry.
- If triage decides Havy, append an `OuterCycle.vN` entry (Havy OuterCycle).
- Append a new `OuterCycle.vN` entry after each **full** outer cycle.
- A cycle is not “completed” unless Level1, Level2, and Level3 were executed and merged.
- Do not rewrite history. If you need to correct something, add an `Amendment.vN` entry.
- Each cycle entry must be self-auditable: versions, verification, gates, evidence pointers.

---

## RequestTriage.v1

- Timestamp:
- Request summary (1–3 lines):
- Decision: Lite / Havy
- Reasons (max 3 bullets):
  - (reason)
- Files read:
  - `.tbrpwn/tbr/TARGET.md`
  - `.tbrpwn/tbr/BEHAVE.md`
  - `.tbrpwn/tbr/REMEMBER.md`

---

## LiteCycle.v1

- Cycle start timestamp:
- Cycle end timestamp:
- Summary (1–3 lines):

### Versions updated (Lite)

PWN versions:

- Level2: PLAN.v? / WORK.v? / NOTE.v?

TBR versions:

- BEHAVE.v?
- REMEMBER.v?

Conditional (only if changed):

- TARGET.v?

### Required file proof (Lite minimum)

- [ ] `.tbrpwn/pwn/level2/PLAN.md` -> PLAN.v?
- [ ] `.tbrpwn/pwn/level2/WORK.md` -> WORK.v?
- [ ] `.tbrpwn/pwn/level2/NOTE.md` -> NOTE.v?
- [ ] `.tbrpwn/tbr/BEHAVE.md` -> BEHAVE.v?
- [ ] `.tbrpwn/tbr/REMEMBER.md` -> REMEMBER.v?
- [ ] `.tbrpwn/LOG.md` -> LiteCycle.v?

Conditional (only if changed):

- [ ] `.tbrpwn/tbr/TARGET.md` -> TARGET.v?

### Lite execution checklist

- [ ] Level2 PWN executed; updated `.tbrpwn/pwn/level2/{PLAN,WORK,NOTE}.md`
- [ ] Level2 merged into `.tbrpwn/tbr/{BEHAVE,REMEMBER}.md`
- [ ] Gate check results recorded in any updated TBR files
- [ ] Verification executed (or explicitly marked impossible with reason)
- [ ] This LiteCycle entry is appended (no rewriting)

### Verification

- Command/check:
  - Expected pass signal:
  - Result: PASS / FAIL
  - Output pointer: (file path / pasted excerpt)

### Evidence pointers (top-level) — LiteCycle

- (file path / command output)

---

## OuterCycle.v1

- Cycle start timestamp:
- Cycle end timestamp:
- Promote used: `promote/promote.tbrpwn.<type>.md`
- Summary (1–3 lines):

### Versions updated (required)

Record the latest versions after this cycle.

PWN versions:

- Level1: PLAN.v? / WORK.v? / NOTE.v?
- Level2: PLAN.v? / WORK.v? / NOTE.v?
- Level3: PLAN.v? / WORK.v? / NOTE.v?

TBR versions:

- TARGET.v?
- BEHAVE.v?
- REMEMBER.v?

### Required file proof (must be all 13)

List every required runtime file you actually modified in this cycle, with the latest version tag written.

- [ ] `.tbrpwn/tbr/TARGET.md` -> TARGET.v?
- [ ] `.tbrpwn/tbr/BEHAVE.md` -> BEHAVE.v?
- [ ] `.tbrpwn/tbr/REMEMBER.md` -> REMEMBER.v?

- [ ] `.tbrpwn/pwn/level1/PLAN.md` -> PLAN.v?
- [ ] `.tbrpwn/pwn/level1/WORK.md` -> WORK.v?
- [ ] `.tbrpwn/pwn/level1/NOTE.md` -> NOTE.v?

- [ ] `.tbrpwn/pwn/level2/PLAN.md` -> PLAN.v?
- [ ] `.tbrpwn/pwn/level2/WORK.md` -> WORK.v?
- [ ] `.tbrpwn/pwn/level2/NOTE.md` -> NOTE.v?

- [ ] `.tbrpwn/pwn/level3/PLAN.md` -> PLAN.v?
- [ ] `.tbrpwn/pwn/level3/WORK.md` -> WORK.v?
- [ ] `.tbrpwn/pwn/level3/NOTE.md` -> NOTE.v?

- [ ] `.tbrpwn/LOG.md` -> OuterCycle.v?

### Execution checklist (must all be true)

- [ ] Level1 PWN executed; updated `.tbrpwn/pwn/level1/{PLAN,WORK,NOTE}.md`
- [ ] Level1 merged into `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md`
- [ ] Level2 PWN executed; updated `.tbrpwn/pwn/level2/{PLAN,WORK,NOTE}.md`
- [ ] Level2 merged into `.tbrpwn/tbr/{BEHAVE,REMEMBER}.md`
- [ ] Level3 PWN executed; updated `.tbrpwn/pwn/level3/{PLAN,WORK,NOTE}.md`
- [ ] Level3 merged into `.tbrpwn/tbr/REMEMBER.md`
- [ ] Gate check results recorded in `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md`
- [ ] Verification executed (or explicitly marked impossible with reason)
- [ ] This cycle entry is appended (no rewriting)

### Verification (required)

List the exact checks you used and the pass/fail signal.

- Command/check:

  - Expected pass signal:
  - Result: PASS / FAIL
  - Output pointer: <file path / pasted excerpt>

If verification is impossible:

- Reason:
- What you recorded instead (evidence plan):

### Gate results (copy from `.tbrpwn/tbr/*`)

Copy the results and evidence pointers from the Gate check result blocks.

- TARGET: PASS / FAIL

  - Evidence pointers:
    - (pointer)
  - BEHAVE: PASS / FAIL

  - Evidence pointers:
    - (pointer)
  - REMEMBER: PASS / FAIL

  - Evidence pointers:
    - (pointer)

### What changed (minimal diff summary)

- TARGET acceptance changes:

  - (checked/added/split item)
- BEHAVE step change (one step only):

  - (from → to)
- REMEMBER compression/decisions:

  - (what was added/removed)

### Evidence pointers (top-level) — OuterCycle

- (file path / command output)

### Decisions

- (decision) — why

### Blockers / risks

- (blocker)

### Next BEHAVE step

- (one step, copied from `.tbrpwn/tbr/BEHAVE.md`)

---

## Amendment.v1

- Timestamp:
- Applies to: OuterCycle.v?
- Correction:
- Evidence pointer:
