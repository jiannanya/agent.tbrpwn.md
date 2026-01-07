# promote.tbrpwn.product.md — TBR-PWN (Product Delivery)

## Target (fill first)
**TARGET.v1**
- Product request:
- Target users:
- Must-have behaviors:
- Constraints:
- Acceptance:
  - [ ] Spec captured (flows + inputs/outputs)
  - [ ] Implementation complete
  - [ ] Verification executed
  - [ ] Packaging + usage documented

## Behave (derive each iteration)
**BEHAVE.vN**
- Step (one step only): spec | scaffold | implement | integrate | document | verify
- Verification: unit/integration/minimal e2e
- Rollback: revert to last good checkpoint

## Remember (persist minimal state)
**REMEMBER.vN**
- Spec decisions:
- What’s implemented:
- Verification evidence:
- Known limitations:

---

## TBR-PWN product rules
- Level1 refines spec into acceptance checkboxes + the next smallest step.
- Level2 iterates implement/verify one step at a time.
- Level3 compresses REMEMBER to spec decisions + evidence + limitations.

## Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.

## Target update policy
- Split features into checkboxes; never hide work inside vague acceptance.
- Require runnable verification before marking “done”.
