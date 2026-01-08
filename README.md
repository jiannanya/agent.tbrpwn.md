# agent.tbrpwn: TBR-PWN AI Agent Loop Promote Engineering

`agent.tbrpwn` is a file-driven workflow for running an AI agent (or a team) with **high auditability** and **low drift**.

**It treats an AI agent as both human-like and machine-like and therefore introduces a TBR-PWN loop.**

It combines:
- **Human-like TBR outer loop**: `TARGET → BEHAVE → REMEMBER` as stable states on disk.
- **Machine-like PWN inner loop**: `PLAN → WORK → NOTE` inside each phase to iterate without losing rigor.

Key Note:
- **TBR essentially simulates the process by which humans explore and handle a task or solve a problem.**
- **PWN is introduced to enhance the divergent and iterative capabilities of TBR.**

This folder is designed to be copied into a project and used as the operational contract for an AI coding/automation/research agent.

---

## Table of Contents

- [agent.tbrpwn: TBR-PWN AI Agent Loop Promote Engineering](#agenttbrpwn-tbr-pwn-ai-agent-loop-promote-engineering)
  - [Table of Contents](#table-of-contents)
  - [What you get](#what-you-get)
  - [Start here](#start-here)
  - [Bootstrap / reset runtime state](#bootstrap--reset-runtime-state)
  - [Folder layout](#folder-layout)
    - [Outer loop state (authoritative)](#outer-loop-state-authoritative)
    - [Inner loop state (phase-local)](#inner-loop-state-phase-local)
    - [Per-cycle log (required)](#per-cycle-log-required)
  - [The workflow (outer loop)](#the-workflow-outer-loop)
    - [Outer cycle](#outer-cycle)
    - [Stop condition (objective)](#stop-condition-objective)
  - [The workflow (inner PWN loop)](#the-workflow-inner-pwn-loop)
    - [Required versioning](#required-versioning)
    - [Meaningful PLAN change (strict)](#meaningful-plan-change-strict)
    - [PLAN stability (stop condition for a level)](#plan-stability-stop-condition-for-a-level)
    - [Anti-stall rule](#anti-stall-rule)
  - [Quality gates (objective + auditable)](#quality-gates-objective--auditable)
    - [Per-cycle requirement](#per-cycle-requirement)
    - [Hard rule (do not violate)](#hard-rule-do-not-violate)
  - [Merge rules (provable)](#merge-rules-provable)
  - [How to use this with an AI agent (suggested)](#how-to-use-this-with-an-ai-agent-suggested)
  - [Common usage patterns](#common-usage-patterns)
  - [Where to customize](#where-to-customize)
  - [Principle Explanation](#principle-explanation)

## What you get

- A strict, repeatable loop that converges:
  - PLAN converges via “meaningful change” + “two consecutive stable versions”.
  - Outer cycle converges via “acceptance complete + TARGET no longer changes”.
- A merge discipline that prevents hand-wavy completion.
- **Quality gates** with explicit **PASS/FAIL** and required evidence pointers.

---

## Start here

1) Read the entry point:
- `promote/promote.tbrpwn.main.md`

2) Or if you want the full operating contract (recommended for agents), read:
- `agent.tbrpwn.md`

3) Or choose exactly one type-specific promote:
- `promote/promote.tbrpwn.coding.md`
- `promote/promote.tbrpwn.debugging.md`
- `promote/promote.tbrpwn.research.md`
- `promote/promote.tbrpwn.product.md`
- `promote/promote.tbrpwn.automation.md`

---

## Bootstrap / reset runtime state

Runtime state must live under `.tbrpwn/`.

If `.tbrpwn/` already exists, do not re-copy templates—just keep updating `.tbrpwn/*`.

If you need to start fresh:
- Delete `.tbrpwn/`.
- Recreate it by copying templates from `tbr/` and `pwn/` (or restore from your VCS).
- Then initialize `.tbrpwn/tbr/TARGET.md` and begin the loop.

---

## Folder layout

Runtime state location:
- All execution updates must go under `.tbrpwn/`.
- Repo-root `tbr/` and `pwn/` are templates/reference.

### Outer loop state (authoritative)
- `.tbrpwn/tbr/TARGET.md`
  - Goal, constraints, non-goals, acceptance checkboxes (with evidence expectation), blocking questions.
  - Includes an objective **quality gate** + per-cycle **Gate check result**.
- `.tbrpwn/tbr/BEHAVE.md`
  - Exactly **one smallest next step** (with verify + rollback).
  - Includes quality gate + Gate check result.
- `.tbrpwn/tbr/REMEMBER.md`
  - Minimal durable memory: facts, decisions, evidence pointers, blocker, risks.
  - Includes quality gate + Gate check result.

### Inner loop state (phase-local)
- `.tbrpwn/pwn/level1/{PLAN,WORK,NOTE}.md` — Target phase PWN
- `.tbrpwn/pwn/level2/{PLAN,WORK,NOTE}.md` — Behave phase PWN
- `.tbrpwn/pwn/level3/{PLAN,WORK,NOTE}.md` — Remember phase PWN

### Per-cycle log (required)
- `.tbrpwn/LOG.md` — append after each full outer cycle.

Each level’s `WORK.md` contains a **merge-proof checklist** used as the merge audit trail.

---

## The workflow (outer loop)

Repeat outer cycles until “Stop condition”.

### Outer cycle
1) **Target phase**: run Level1 PWN until Level1 PLAN stabilizes → merge into `.tbrpwn/tbr/TARGET.md`, `.tbrpwn/tbr/BEHAVE.md`, `.tbrpwn/tbr/REMEMBER.md`.
2) **Behave phase**: run Level2 PWN until Level2 PLAN stabilizes → merge into `.tbrpwn/tbr/BEHAVE.md`, `.tbrpwn/tbr/REMEMBER.md`.
3) **Remember phase**: run Level3 PWN until Level3 PLAN stabilizes → merge into `.tbrpwn/tbr/REMEMBER.md`.
4) **Derive next TARGET** using current `.tbrpwn/tbr/BEHAVE.md` + `.tbrpwn/tbr/REMEMBER.md`.
5) Append `.tbrpwn/LOG.md` for the completed cycle.

### Stop condition (objective)
Stop only when both are true:
- `.tbrpwn/tbr/TARGET.md` acceptance is complete (every acceptance checkbox has evidence).
- A full outer cycle would not change `.tbrpwn/tbr/TARGET.md`.

---

## The workflow (inner PWN loop)

Within a single phase, repeat PWN until the PLAN converges.

### Required versioning
Every PWN file is versioned:
- `PLAN.vN`, `WORK.vN`, `NOTE.vN`
- Each new version must include **Delta since v(N-1)**.

### Meaningful PLAN change (strict)
A PLAN update is meaningful only if it changes at least one:
- Task set (add/remove/merge/split)
- Ordering/dependencies
- Success criteria / verification signals
- Risk controls (rollback/safety constraints)

Pure rewording is not meaningful.

### PLAN stability (stop condition for a level)
PLAN is stable when **two consecutive PLAN versions** have **no meaningful delta**.

### Anti-stall rule
If PLAN is stable but WORK is incomplete:
- Execute WORK.
- Update NOTE with objective outputs.
- Do not keep “planning”.

---

## Quality gates (objective + auditable)

Each outer file contains its own “Quality gate (objective)” checklist.

### Per-cycle requirement
Each outer cycle must record a **Gate check result** inside:
- `.tbrpwn/tbr/TARGET.md`
- `.tbrpwn/tbr/BEHAVE.md`
- `.tbrpwn/tbr/REMEMBER.md`

### Hard rule (do not violate)
You may only claim “passes quality gate” if:
- The file’s Gate check result is `PASS`, and
- The evidence pointers list is non-empty.

If evidence pointers are empty, the Gate check result must be `FAIL`.

---

## Merge rules (provable)

When a level ends (PLAN stable), merge back into TBR and use the merge-proof checklist:
- Level1 merge checklist: `.tbrpwn/pwn/level1/WORK.md`
- Level2 merge checklist: `.tbrpwn/pwn/level2/WORK.md`
- Level3 merge checklist: `.tbrpwn/pwn/level3/WORK.md`

Rule: If you cannot check an item honestly, do not check it. Fix the gap.

---

## How to use this with an AI agent (suggested)

- Open `agent.tbrpwn.md` and treat it as the agent’s system-level contract.
- Keep `.tbrpwn/tbr/` as the only “source of truth”.
- Use `.tbrpwn/pwn/` as disposable iteration state.
- Make the agent include evidence pointers (file paths / command outputs) before marking anything “done”.

---

## Common usage patterns

- Coding: lock build/test commands early; shrink steps until verifiable.
- Debugging: enforce repro steps + hypotheses + experiments with expected signals.
- Research: enforce baselines, explicit metrics, and reproducibility notes.
- Product: enforce spec → implement → verify; keep acceptance checkable.
- Automation: enforce idempotency, external IDs, and audit evidence.

See the matching `promote/promote.tbrpwn.*.md` for the per-domain constraints.

---

## Where to customize

If you copy this folder into a new project, typical customizations are:
- Add repo-specific verification commands to `.tbrpwn/tbr/BEHAVE.md`.
- Adjust acceptance items in `.tbrpwn/tbr/TARGET.md` for the project.
- Keep `.tbrpwn/tbr/REMEMBER.md` short by compressing aggressively.

Avoid loosening the hard rules unless you also loosen acceptance expectations.


##  Principle Explanation
**1. Target Phase:**

The user provides an initial target. The LLM begins the level 1 plan–work–note loop based on this target. The level 1 loop is essentially a variant of the built-in TBR loop, with the goal of refining target, behave, and remember.

The level 1 plan starts by generating a plan from the initial target, which then updates the level 1 work. During the planning process, the level 1 note is also updated with written records. Based on the level 1 plan and level 1 note, the system executes the level 1 work. While performing the work, the level 1 note is updated again. Then, based on the results of the level 1 work and the level 1 note, the level 1 plan is updated. The new plan leads to updates in the level 1 work and level 1 note.

This cycle continues until the level 1 plan no longer updates, at which point the level 1 PWN loop is complete. At the end of the level 1 PWN loop, the current level 1 plan, work, and note are used to update target, behave, and remember. The TBR loop then enters the behave phase.

**2. Behave Phase:**

The LLM executes the level 2 PWN loop based on the current target, behave, and remember. The goal of the level 2 PWN loop is to refine behave and remember.

The system updates the level 2 plan according to the current target, behave, and remember. Then, based on the level 2 plan, it updates the level 2 work and level 2 note. Using the level 2 plan and note, the system executes the level 2 work. During the work process, the level 2 note is updated again. Based on the results of the level 2 work and the level 2 note, a new level 2 plan is generated. The new plan leads to updates in the level 2 work and note.

This cycle continues until the level 2 plan no longer updates, at which point the level 2 PWN loop is complete. At the end of the level 2 PWN loop, the current level 2 plan, work, and note are used to update behave and remember. The TBR loop then enters the remember phase.

**3. Remember Phase:**

The LLM executes the level 3 PWN loop based on the current target, behave, and remember. The goal of the level 3 PWN loop is to refine remember.

The system updates the level 3 plan according to the current target, behave, and remember. Then, based on the level 3 plan, it updates the level 3 work and level 3 note. Using the level 3 plan and note, the system executes the level 3 work. During the work process, the level 3 note is updated again. Based on the results of the level 3 work and the level 3 note, a new level 3 plan is generated. The new plan leads to updates in the level 3 work and note.

This cycle continues until the level 3 plan no longer updates, at which point the level 3 PWN loop is complete. At the end of the level 3 PWN loop, the current level 3 plan, work, and note are used to update remember.

Finally, based on the current behave and remember, a new target is generated. The system then re-enters the initial target phase, repeating the cycle. The process continues until the target is fully achieved and no longer updates, at which point the entire TBR–PWN loop ends.