# promote.tbrpwn.base.md — Target–Behave–Remember with Plan–Work–Note inner loops

## Purpose
Strengthen the TBR loop by embedding a PWN loop inside each phase:
- **TBR**: stable, minimal state that persists across cycles.
- **PWN**: controlled divergence (NOTES) + concrete execution (WORK) + convergent planning (PLAN).

## Definitions
- **Target**: current goal + constraints + acceptance.
- **Behave**: the next-step operating policy derived from Target.
- **Remember**: minimal persistent memory (facts, decisions, evidence, blockers, risks).
- **Plan**: an evolving plan for a single phase.
- **Work**: executable actions/artifacts for the plan.
- **Note**: phase-local scratchpad (observations, alternatives, measurements, questions).

## Global rules (non-negotiable)
- Do not invent facts. If you didn’t read it or run it, don’t claim it.
- Keep iterations small and verifiable.
- Prefer idempotent actions; make retries safe.
- PWN ends only when PLAN stabilizes (not when “it feels done”).
- At PWN completion, merge (PLAN/WORK/NOTE) back into TBR according to the phase.
- All execution updates must be written under `.tbrpwn/`.
- After each full outer cycle, append `.tbrpwn/LOG.md`.

Runtime bootstrap (required):
- If `.tbrpwn/` is missing or corrupted, recreate it by copying the templates from `tbr/` and `pwn/` (or restore from VCS).
- Do not edit the template folders (`tbr/`, `pwn/`) during execution.

---

## PWN semantics (strict)

### Meaningful PLAN update
PLAN is “updated” only if at least one changes:
- Task set: add/remove/merge/split tasks
- Ordering/dependencies
- Success criteria / verification signals
- Risk controls: rollback/safety constraints

Pure rewording is NOT a meaningful update.

### PLAN stability (stop condition)
PLAN is **stable** when two consecutive PLAN versions have no meaningful delta.

### WORK and NOTE discipline
- WORK must be executable steps and artifacts (not analysis).
- NOTE may be exploratory, but MUST be merged or deleted at the end of the phase.
- While executing WORK, keep NOTE updated with objective outputs and observations.

### Anti-stall rule
If PLAN is stable but WORK is incomplete, execute WORK and update NOTE.

### Merge rule at PWN completion
When a level’s PLAN becomes stable, perform a merge back into TBR:
- Promote durable facts + evidence into REMEMBER.
- Convert stable decisions into TARGET/BEHAVE/REMEMBER as appropriate.
- Keep BEHAVE to “one smallest step only”.

Additional constraint:
- TARGET/BEHAVE/REMEMBER must pass their explicit quality gates (see `.tbrpwn/tbr/*.md`).
- Hard rule: you may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

---

## Outer loop: TBR-PWN (repeat until TARGET completes)

### Phase 1: Target phase (Level1 PWN)
**Input**: user-provided init target in `.tbrpwn/tbr/TARGET.md`.

Goal: refine TARGET/BEHAVE/REMEMBER enough to start execution.

**At completion (merge)**:
- Update `.tbrpwn/tbr/TARGET.md`
- Update `.tbrpwn/tbr/BEHAVE.md`
- Update `.tbrpwn/tbr/REMEMBER.md`

**Level1 merge checklist**
Update `.tbrpwn/tbr/TARGET.md`:
- Goal: one sentence
- Constraints: only hard constraints
- Non-goals: explicit scope exclusions
- Acceptance: checkable items with clear evidence expectations
- Open questions: only blocking questions

Update `.tbrpwn/tbr/BEHAVE.md`:
- Next step: exactly one smallest action
- What to touch: concrete artifacts/files
- Verify: objective pass signal
- Rollback + safety: explicit and minimal

Update `.tbrpwn/tbr/REMEMBER.md`:
- Confirmed facts: only with evidence pointers
- Decisions: only durable decisions + rationale
- Evidence plan: if evidence doesn’t exist yet, define how it will be produced
- Blockers/risks: concise and actionable

### Phase 2: Behave phase (Level2 PWN)
**Input**: current `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md`.

Goal: improve BEHAVE and REMEMBER so execution is safe, minimal, and verifiable.

**At completion (merge)**:
- Update `.tbrpwn/tbr/BEHAVE.md`
- Update `.tbrpwn/tbr/REMEMBER.md`

**Level2 merge checklist**
Update `.tbrpwn/tbr/BEHAVE.md`:
- Next step: remain one step; split if it grew
- Verify: exact commands/checks + pass signal
- Rollback: reversible path
- What to touch: precise list

Update `.tbrpwn/tbr/REMEMBER.md`:
- Facts: only what WORK produced/observed
- Decisions: record execution-time decisions + why
- Evidence: minimal excerpt or pointer
- Risks/limitations: new discoveries only

### Phase 3: Remember phase (Level3 PWN)
**Input**: current `.tbrpwn/tbr/{TARGET,BEHAVE,REMEMBER}.md`.

Goal: make REMEMBER minimal, correct, and maximally useful.

**At completion (merge)**:
- Update `.tbrpwn/tbr/REMEMBER.md`

**Level3 merge checklist**
Update `.tbrpwn/tbr/REMEMBER.md`:
- Delete stale assumptions and redundant notes
- Convert vague statements into evidence pointers
- Keep only: facts, decisions, evidence, blockers, risks
- Keep it short (signals, not transcripts)

### Phase 4: Derive next TARGET
Derive the next TARGET from current BEHAVE+REMEMBER:
- Mark acceptance items done only with evidence
- Split large targets
- Refine constraints based on what actually happened

Return to Phase 1 unless TARGET no longer changes and acceptance is complete.
