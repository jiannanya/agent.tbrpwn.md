# agent.tbrpwn.impl.md — AI Agent Contract (Lite + Havy TBR-PWN)

You are an AI agent operating in this repository using the **TBR-PWN** promote engineering workflow.

This contract defines two execution modes:

- **Lite TBR PWN Loop** — optimized for simple, low-risk, small-scope requests.
- **Havy TBR PWN Loop** — the existing strict full-cycle workflow (formerly the default TBR-PWN loop).

Every request must be routed through a Lite triage first, then you must run **either** Lite or Havy accordingly.

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

## 0.1) Per-request routing contract (hard)

This repository is designed for **tool-capable agents** (VS Code Copilot Agent / Claude Code / similar) that can read and write workspace files.

**Hard rule:** For every user request that asks you to “do work” (code, docs, automation, debugging, research), you must:

1) Run the **Lite triage** (Section 0.2) and record the decision.
2) If the request is **Lite**, run **one LiteCycle** (Section 0.3) and persist it to disk.
3) If the request is **Havy**, run **exactly one full Havy OuterCycle** (existing workflow; Section 0.4) and persist it to disk.

An answer is considered **invalid** unless the chosen cycle is completed and the required files below have been updated.

Important:
- Lite requests must NOT be forced through the Havy full OuterCycle.
- Havy requests must NOT be “under-executed” using Lite.

---

## 0.2) Lite triage (decide Lite vs Havy)

You must decide Lite vs Havy at the start of every request.

### Inputs (must read)

- The user request.
- `.tbrpwn/tbr/TARGET.md`, `.tbrpwn/tbr/BEHAVE.md`, `.tbrpwn/tbr/REMEMBER.md`.

### Decision rule

Classify as **Havy** if ANY of the following are true:

- Touches many files or multiple subsystems (roughly: >3 files or >1 subsystem).
- Requires non-trivial design decisions, refactors, or new architecture.
- Involves debugging with uncertain root cause.
- Has meaningful safety/compliance/security risk.
- Requires new tests/build steps or could easily break the repo.
- The user’s goal includes “framework”, “scaffold”, “end-to-end”, “optimize”, “harden”, “refactor”, “benchmark”, etc.

Otherwise classify as **Lite**.

### Required triage record (must persist)

Append a `RequestTriage.vN` entry to `.tbrpwn/LOG.md` containing:

- Request summary (1–3 lines)
- Decision: `Lite` or `Havy`
- Reasons (3 bullets max)
- Which files you read

If you cannot append to `.tbrpwn/LOG.md`, output `BLOCKED`.

---

## 0.3) Lite TBR PWN Loop (LiteCycle)

Lite is a **Behave-centric** micro-cycle intended for simple tasks.

### LiteCycle definition (must all be true)

- Uses **Level2 PWN only** (Behave phase): `.tbrpwn/pwn/level2/{PLAN,WORK,NOTE}.md`.
- Updates `.tbrpwn/tbr/BEHAVE.md` (one smallest step) and `.tbrpwn/tbr/REMEMBER.md` (evidence + decisions).
- Updates `.tbrpwn/tbr/TARGET.md` only if acceptance/constraints truly changed.
- Records Gate check results in any TBR file you updated.
- Appends a `LiteCycle.vN` entry to `.tbrpwn/LOG.md`.

### Required on-disk updates (Lite minimum)

You must update all of the following:

- `.tbrpwn/pwn/level2/PLAN.md`
- `.tbrpwn/pwn/level2/WORK.md`
- `.tbrpwn/pwn/level2/NOTE.md`
- `.tbrpwn/tbr/BEHAVE.md`
- `.tbrpwn/tbr/REMEMBER.md`
- `.tbrpwn/LOG.md`

And conditionally:

- `.tbrpwn/tbr/TARGET.md` (only if it truly changes)

### Lite completion proof (copy/paste)

For Lite, include this checklist in both the `LiteCycle.vN` log entry and your final response:

```text
LiteCycle appended: LiteCycle.v?

Required files updated (Lite minimum):
- [ ] .tbrpwn/pwn/level2/PLAN.md -> PLAN.v?
- [ ] .tbrpwn/pwn/level2/WORK.md -> WORK.v?
- [ ] .tbrpwn/pwn/level2/NOTE.md -> NOTE.v?
- [ ] .tbrpwn/tbr/BEHAVE.md -> BEHAVE.v?
- [ ] .tbrpwn/tbr/REMEMBER.md -> REMEMBER.v?
- [ ] .tbrpwn/LOG.md -> LiteCycle.v?

Conditional (only if changed):
- [ ] .tbrpwn/tbr/TARGET.md -> TARGET.v?
```

### LiteCycle runbook (mandatory)

1) Update Level2 `PLAN` (max 2 iterations), ensuring verification + rollback exist.
2) Do the smallest WORK that makes progress and is verifiable.
3) Update NOTE with objective outputs (files/commands/results).
4) Merge into BEHAVE (one step only) and REMEMBER (durable evidence).
5) Record Gate check result blocks in updated TBR files.
6) Append `LiteCycle.vN` to `.tbrpwn/LOG.md`.

If at any point the task expands beyond Lite scope, immediately reclassify as Havy and switch to Section 0.4.

---

## 0.4) Havy TBR PWN Loop (Havy OuterCycle)

Havy is the original strict TBR-PWN workflow: run Level1 + Level2 + Level3 and merge into TBR.

If (and only if) the triage decision is **Havy**, the remainder of this document defines the Havy contract.

### Definition: “One full Havy OuterCycle” (must all be true)

- Level1 PWN executed and merged.
- Level2 PWN executed and merged.
- Level3 PWN executed and merged.
- Gate check results recorded in `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md` for this cycle.
- `.tbrpwn/LOG.md` appended with a new `OuterCycle.vN` entry.

### Required on-disk updates (minimum set)

You must write updates to **all** of the following files in the workspace:

- `.tbrpwn/tbr/TARGET.md`
- `.tbrpwn/tbr/BEHAVE.md`
- `.tbrpwn/tbr/REMEMBER.md`
- `.tbrpwn/pwn/level1/PLAN.md`, `.tbrpwn/pwn/level1/WORK.md`, `.tbrpwn/pwn/level1/NOTE.md`
- `.tbrpwn/pwn/level2/PLAN.md`, `.tbrpwn/pwn/level2/WORK.md`, `.tbrpwn/pwn/level2/NOTE.md`
- `.tbrpwn/pwn/level3/PLAN.md`, `.tbrpwn/pwn/level3/WORK.md`, `.tbrpwn/pwn/level3/NOTE.md`
- `.tbrpwn/LOG.md`

If a phase genuinely produces “no change”, you must still append a new versioned section (at minimum a `NOTE.vN`) that records what you checked and why no change was needed.

### Version bump rule (anti-stall, anti-pretend)

For each full Havy outer cycle you complete, you must ensure the cycle produces a new version in each required file:

- In `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md`, append a new top-level `TARGET.vN` / `BEHAVE.vN` / `REMEMBER.vN` section.
- In each PWN file, append a new `PLAN.vN` / `WORK.vN` / `NOTE.vN` section.
- In `.tbrpwn/LOG.md`, append a new `OuterCycle.vN` entry.

If you cannot produce a meaningful new version (e.g., because you cannot read/write files), you must use `BLOCKED`.

### Tooling requirement (no pretending)

- You must actually read the above files at the start of the cycle.
- You must actually edit/write the above files during the cycle.
- If the environment does not allow file I/O tools, you must stop and output `BLOCKED` (see below).

### Completion proof (required)

To prevent “the agent said it updated files but didn’t”, every completed cycle must include explicit proof:

- In `.tbrpwn/LOG.md` `OuterCycle.vN`, fill `Versions updated` fields with the latest versions you wrote.
- In the same log entry, the `Evidence pointers (top-level)` list must include the full list of required files you modified.
- In your final response to the user, you must repeat:
  - Which `OuterCycle.vN` was appended.
  - The full list of `.tbrpwn/*` files modified.
  - The latest version tags you wrote (e.g., `TARGET.v2`, `Level2 PLAN.v3`, etc.).

If you cannot provide this proof, treat the cycle as incomplete and output `BLOCKED`.

#### Havy required file proof template (copy/paste)

Every completed outer cycle must include this exact checklist (filled) in both:

- the new `.tbrpwn/LOG.md` `OuterCycle.vN` entry, and
- your final response to the user.

Fill each line with the latest version tag you wrote in that file.

```text
HavyOuterCycle appended: OuterCycle.v?

Required files updated (must be all 13):
- [ ] .tbrpwn/tbr/TARGET.md -> TARGET.v?
- [ ] .tbrpwn/tbr/BEHAVE.md -> BEHAVE.v?
- [ ] .tbrpwn/tbr/REMEMBER.md -> REMEMBER.v?

- [ ] .tbrpwn/pwn/level1/PLAN.md -> PLAN.v?
- [ ] .tbrpwn/pwn/level1/WORK.md -> WORK.v?
- [ ] .tbrpwn/pwn/level1/NOTE.md -> NOTE.v?

- [ ] .tbrpwn/pwn/level2/PLAN.md -> PLAN.v?
- [ ] .tbrpwn/pwn/level2/WORK.md -> WORK.v?
- [ ] .tbrpwn/pwn/level2/NOTE.md -> NOTE.v?

- [ ] .tbrpwn/pwn/level3/PLAN.md -> PLAN.v?
- [ ] .tbrpwn/pwn/level3/WORK.md -> WORK.v?
- [ ] .tbrpwn/pwn/level3/NOTE.md -> NOTE.v?

- [ ] .tbrpwn/LOG.md -> OuterCycle.v?
```

### BLOCKED protocol (when you cannot complete the cycle)

If you cannot read/write `.tbrpwn/*` (missing workspace, permissions, tools disabled, etc.), do not “simulate” updates.

Instead output:

- `BLOCKED: cannot complete Havy OuterCycle`
- Reason (one line)
- What you need from the user (one line)
- Which required files could not be read/written (list)

---

## Bootstrapping the workspace (runtime)

- During execution, write Lite + Havy TBR-PWN updates only under `.tbrpwn/`.
- Treat repo-root `tbr/` and `pwn/` as templates/reference.

If `.tbrpwn/` is missing:

- Recreate it by copying the templates from `tbr/` and `pwn/` (or restore from VCS).
- Initialize `.tbrpwn/tbr/TARGET.md` and start the outer cycle.

---

## 1) What “done” means

You may stop only when **both** are true:

- `.tbrpwn/tbr/TARGET.md` acceptance is complete (every acceptance checkbox has evidence).
- A full outer cycle would not change `.tbrpwn/tbr/TARGET.md`.

Do not stop because work “feels complete”.

---

## 2) Source of truth (files)

### Outer loop state (authoritative)

- `.tbrpwn/tbr/TARGET.md` — goal, constraints, non-goals, acceptance, blocking questions.
- `.tbrpwn/tbr/BEHAVE.md` — exactly one next step, with verification + rollback.
- `.tbrpwn/tbr/REMEMBER.md` — minimal durable memory: facts, decisions, evidence pointers, blockers, risks.

### Inner loop state (phase-local)

- `.tbrpwn/pwn/level1/{PLAN,WORK,NOTE}.md` — Target phase PWN
- `.tbrpwn/pwn/level2/{PLAN,WORK,NOTE}.md` — Behave phase PWN
- `.tbrpwn/pwn/level3/{PLAN,WORK,NOTE}.md` — Remember phase PWN

### Required log (append-only)

- `.tbrpwn/LOG.md` — must be appended after each full outer cycle.

### Entry points / policy references

- `promote/promote.tbrpwn.main.md` — choose a type-specific promote.
- `promote/promote.tbrpwn.base.md` — global semantics + merge discipline.
- Type-specific promotes (`promote/promote.tbrpwn.*.md`) — extra constraints for specific domains.

**Rule:** Update TBR PWN files under `.tbrpwn/` during execution. Treat the repo-root `tbr/` and `pwn/` folders as templates/reference. When in doubt, update the outer TBR files, not just PWN notes.

---

## 3) The loop (high-level algorithm)

Repeat outer cycles until stop condition.

**Outer cycle:**

1) **Target phase → Level1 PWN** until Level1 PLAN is stable → merge into `.tbrpwn/tbr/TARGET.md`, `.tbrpwn/tbr/BEHAVE.md`, `.tbrpwn/tbr/REMEMBER.md`.
2) **Behave phase → Level2 PWN** until Level2 PLAN is stable → merge into `.tbrpwn/tbr/BEHAVE.md`, `.tbrpwn/tbr/REMEMBER.md`.
3) **Remember phase → Level3 PWN** until Level3 PLAN is stable → merge into `.tbrpwn/tbr/REMEMBER.md`.
4) **Derive next TARGET** using current `.tbrpwn/tbr/BEHAVE.md` + `.tbrpwn/tbr/REMEMBER.md`.
5) **Append `.tbrpwn/LOG.md`** with the completed outer-cycle entry.

---

## 3.1) OuterCycle runbook (mandatory sequence)

Follow this sequence strictly for each user request.

### Step A — Load runtime state (must read)

Read these files first (do not assume their contents):

- `.tbrpwn/tbr/TARGET.md`, `.tbrpwn/tbr/BEHAVE.md`, `.tbrpwn/tbr/REMEMBER.md`
- `.tbrpwn/pwn/level1/{PLAN,WORK,NOTE}.md`
- `.tbrpwn/pwn/level2/{PLAN,WORK,NOTE}.md`
- `.tbrpwn/pwn/level3/{PLAN,WORK,NOTE}.md`
- `.tbrpwn/LOG.md`

If any are missing, bootstrap `.tbrpwn/` (see Bootstrapping). If you cannot, use `BLOCKED`.

### Step B — Level1 (Target phase) must produce new versions

- Update Level1 `PLAN` until stable (two consecutive PLAN versions with no meaningful delta).
- Apply Anti-stall: if PLAN stable and WORK incomplete, do WORK and update NOTE.
- Complete the Level1 merge-proof checklist in `.tbrpwn/pwn/level1/WORK.md`.
- Merge into `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md`.

If you cannot reach PLAN stability quickly:

- You may iterate PLAN up to 3 times.
- If still not stable, you must proceed by shrinking WORK to the smallest safe, verifiable action, record the limitation in NOTE and REMEMBER, and continue the outer cycle.

### Step C — Level2 (Behave phase) must produce new versions

- Same mechanics as Level1.
- Merge into `.tbrpwn/tbr/{BEHAVE,REMEMBER}.md`.

### Step D — Level3 (Remember phase) must produce new versions

- Same mechanics as Level1.
- Merge into `.tbrpwn/tbr/REMEMBER.md`.

### Step E — Gate checks + verification (must be recorded)

- Record Gate check results (PASS/FAIL + non-empty evidence pointers when PASS) inside:
  - `.tbrpwn/tbr/TARGET.md`
  - `.tbrpwn/tbr/BEHAVE.md`
  - `.tbrpwn/tbr/REMEMBER.md`
- Run verification commands/checks when applicable; if impossible, record the reason in REMEMBER and LOG.

### Step F — Append log entry (must append)

- Append a new `OuterCycle.vN` entry to `.tbrpwn/LOG.md`.
- The log entry must confirm Level1/2/3 executed + merged + gates recorded.
- The log entry must include (1) the latest versions you wrote and (2) the full list of modified `.tbrpwn/*` files as evidence pointers.

### Step G — Response format (tie answer to disk)

In your final response to the user, include:

- The `OuterCycle.vN` you just appended.
- The list of files you modified under `.tbrpwn/`.
- The single next step copied from `.tbrpwn/tbr/BEHAVE.md`.
- The latest version tags you wrote (TBR + PWN).

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

- Level1: `.tbrpwn/pwn/level1/WORK.md`
- Level2: `.tbrpwn/pwn/level2/WORK.md`
- Level3: `.tbrpwn/pwn/level3/WORK.md`

**Rule:** If you cannot check an item honestly, do not check it—fix the gap instead.

---

## 6) Quality gates (objective + auditable)

Each outer file contains its own **Quality gate (objective)** checklist.

### 6.1 Required per outer cycle

Each outer cycle must record **Gate check results** inside:

- `.tbrpwn/tbr/TARGET.md`
- `.tbrpwn/tbr/BEHAVE.md`
- `.tbrpwn/tbr/REMEMBER.md`

### 6.2 Hard rule (do not violate)

You may only claim “passes quality gate” if:

- The file’s **Gate check result** is `PASS`, **and**
- The **Evidence pointers** list is **non-empty**.

If evidence pointers are empty, the Gate check result must be `FAIL`.

---

## 7) How to write each outer file

### 7.1 `.tbrpwn/tbr/TARGET.md`

Keep it unambiguous and checkable:

- **Goal:** one sentence.
- **Constraints:** explicit + testable.
- **Non-goals:** explicit exclusions.
- **Acceptance:** checkboxes with expected evidence.
- **Open questions:** only blocking questions.

### 7.2 `.tbrpwn/tbr/BEHAVE.md`

Must always be **one smallest step**:

- Exactly one step.
- Concrete “what to touch” artifacts.
- Objective verification + pass signal.
- Explicit rollback.

### 7.3 `.tbrpwn/tbr/REMEMBER.md`

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
- If you cannot run required verification: record the limitation explicitly in `.tbrpwn/tbr/REMEMBER.md` and adjust acceptance/verification to what is possible.
- If you are blocked by missing information: add a *blocking question* to `.tbrpwn/tbr/TARGET.md` (do not hide it in NOTE).

---

## 9) Choosing a type-specific promote

Before starting work, pick exactly one of:

- `promote/promote.tbrpwn.coding.md`
- `promote/promote.tbrpwn.debugging.md`
- `promote/promote.tbrpwn.research.md`
- `promote/promote.tbrpwn.product.md`
- `promote/promote.tbrpwn.automation.md`

Then apply its additional rules on top of this contract.

---

## 10) Minimal operational checklist (per outer cycle)

- Update Level1 PWN files until PLAN stable → merge → record gate results in TARGET/BEHAVE/REMEMBER.
- Update Level2 PWN files until PLAN stable → merge → record gate results in BEHAVE/REMEMBER.
- Update Level3 PWN files until PLAN stable → merge → record gate results in REMEMBER.
- Rewrite/derive next TARGET based on BEHAVE+REMEMBER.
- Stop only if TARGET acceptance complete and TARGET no longer changes after a full cycle.
