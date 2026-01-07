# agent.tbrpwn.md — AI Agent Promote (TBR-PWN)

You are an AI agent operating in this repository using the **TBR-PWN** promote engineering workflow.

- **Outer loop (TBR):** stable, minimal, file-driven state.
- **Inner loop (PWN):** iterative Plan→Work→Note inside each phase until the plan converges.

This document is an executable operating contract: follow it literally.

---

## 0) Non-negotiables

- **No invented facts.** If you didn’t read a file or run a command/tool, do not claim it happened.
- **Evidence beats description.** Prefer pointers to files/commands/outputs over narrative.
- **Small, verifiable steps.** Make progress via tiny deltas and objective checks.
- **Idempotency by default.** Prefer actions safe to retry.
- **Stop conditions are objective** (see “Stop condition”).

If a requirement conflicts with this contract, surface the conflict and ask the user.

---

## 1) What “done” means

You may stop only when **both** are true:
- `tbr/TARGET.md` acceptance is complete (every acceptance checkbox has evidence).
- A full outer cycle would not change `tbr/TARGET.md`.

Do not stop because work “feels complete”.

---

## 2) Source of truth (files)

### Outer loop state (authoritative)
- `tbr/TARGET.md` — goal, constraints, non-goals, acceptance, blocking questions.
- `tbr/BEHAVE.md` — exactly one next step, with verification + rollback.
- `tbr/REMEMBER.md` — minimal durable memory: facts, decisions, evidence pointers, blockers, risks.

### Inner loop state (phase-local)
- `pwn/level1/{PLAN,WORK,NOTE}.md` — Target phase PWN
- `pwn/level2/{PLAN,WORK,NOTE}.md` — Behave phase PWN
- `pwn/level3/{PLAN,WORK,NOTE}.md` — Remember phase PWN

### Entry points / policy references
- `promote.tbrpwn.main.md` — choose a type-specific promote.
- `promote.tbrpwn.base.md` — global semantics + merge discipline.
- Type-specific promotes (`promote.tbrpwn.*.md`) — extra constraints for specific domains.

**Rule:** When in doubt, update the outer files, not just PWN notes.

---

## 3) The loop (high-level algorithm)

Repeat outer cycles until stop condition.

**Outer cycle:**
1) **Target phase → Level1 PWN** until Level1 PLAN is stable → merge into `tbr/TARGET.md`, `tbr/BEHAVE.md`, `tbr/REMEMBER.md`.
2) **Behave phase → Level2 PWN** until Level2 PLAN is stable → merge into `tbr/BEHAVE.md`, `tbr/REMEMBER.md`.
3) **Remember phase → Level3 PWN** until Level3 PLAN is stable → merge into `tbr/REMEMBER.md`.
4) **Derive next TARGET** using current `tbr/BEHAVE.md` + `tbr/REMEMBER.md`.

---

## 4) PWN mechanics (strict)

### 4.1 Versioning
In each PWN file, maintain versioned sections:
- `PLAN.vN`
- `WORK.vN`
- `NOTE.vN`

Every new version must include:
- **Delta since v(N-1)** (short and explicit)

### 4.2 Meaningful PLAN update
A PLAN update is meaningful only if at least one changes:
- Task set (add/remove/merge/split tasks)
- Ordering/dependencies
- Success criteria / verification signals
- Risk controls (rollback/safety constraints)

Pure rewording is **not** a meaningful update.

### 4.3 PLAN stability (stop condition for a level)
PLAN is stable when **two consecutive PLAN versions** have **no meaningful delta**.

### 4.4 Anti-stall rule
If PLAN is stable but WORK is incomplete:
- Execute WORK.
- Update NOTE with objective outputs.
- Do **not** keep “planning”.

---

## 5) Merge discipline (must be provable)

When a level ends (PLAN stable), you must merge into outer TBR files.

Use the merge-proof checklists as the audit trail:
- Level1: `pwn/level1/WORK.md`
- Level2: `pwn/level2/WORK.md`
- Level3: `pwn/level3/WORK.md`

**Rule:** If you cannot check an item honestly, do not check it—fix the gap instead.

---

## 6) Quality gates (objective + auditable)

Each outer file contains its own **Quality gate (objective)** checklist.

### 6.1 Required per outer cycle
Each outer cycle must record **Gate check results** inside:
- `tbr/TARGET.md`
- `tbr/BEHAVE.md`
- `tbr/REMEMBER.md`

### 6.2 Hard rule (do not violate)
You may only claim “passes quality gate” if:
- The file’s **Gate check result** is `PASS`, **and**
- The **Evidence pointers** list is **non-empty**.

If evidence pointers are empty, the Gate check result must be `FAIL`.

---

## 7) How to write each outer file

### 7.1 `tbr/TARGET.md`
Keep it unambiguous and checkable:
- **Goal:** one sentence.
- **Constraints:** explicit + testable.
- **Non-goals:** explicit exclusions.
- **Acceptance:** checkboxes with expected evidence.
- **Open questions:** only blocking questions.

### 7.2 `tbr/BEHAVE.md`
Must always be **one smallest step**:
- Exactly one step.
- Concrete “what to touch” artifacts.
- Objective verification + pass signal.
- Explicit rollback.

### 7.3 `tbr/REMEMBER.md`
Keep only durable signal:
- Facts with evidence pointers.
- Decisions with a short “why”.
- Minimal evidence excerpts (prefer pointers).
- Current status: PASS/FAIL + current blocker.
- Risks/limitations.

Do not store raw chat logs or long transcripts.

---

## 8) Handling uncertainty, failures, and blockers

- If a step is risky or unclear: **shrink the step** until it becomes safe and verifiable.
- If you cannot run required verification: record the limitation explicitly in `tbr/REMEMBER.md` and adjust acceptance/verification to what is possible.
- If you are blocked by missing information: add a *blocking question* to `tbr/TARGET.md` (do not hide it in NOTE).

---

## 9) Choosing a type-specific promote

Before starting work, pick exactly one of:
- `promote.tbrpwn.coding.md`
- `promote.tbrpwn.debugging.md`
- `promote.tbrpwn.research.md`
- `promote.tbrpwn.product.md`
- `promote.tbrpwn.automation.md`

Then apply its additional rules on top of this contract.

---

## 10) Minimal operational checklist (per outer cycle)

- Update Level1 PWN files until PLAN stable → merge → record gate results in TARGET/BEHAVE/REMEMBER.
- Update Level2 PWN files until PLAN stable → merge → record gate results in BEHAVE/REMEMBER.
- Update Level3 PWN files until PLAN stable → merge → record gate results in REMEMBER.
- Rewrite/derive next TARGET based on BEHAVE+REMEMBER.
- Stop only if TARGET acceptance complete and TARGET no longer changes after a full cycle.
