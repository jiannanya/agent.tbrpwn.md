# PWN (Plan–Work–Note) — Runtime

This folder contains the **runtime** PWN state for the current outer cycle.

Rules:
- Update these files during execution; do not edit the root `pwn/` templates.
- Maintain versioned sections (`*.vN`) and explicit deltas.
- After each level ends (PLAN stable), merge into `.tbrpwn/tbr/*` and then record the cycle in `.tbrpwn/LOG.md`.

Quality gates (hard rule)
- You may only claim “passes quality gate” if the file’s Gate check result is `PASS` AND the evidence pointers list is non-empty.
