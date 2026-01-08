# .tbrpwn (Runtime State)

This folder contains the **runtime** state for the TBR-PWN loop.

- Treat files under `.tbrpwn/` as the **only** files that should be updated during execution.
- Treat `tbr/` and `pwn/` at the repo root as **templates/reference**.

## Contents

- `.tbrpwn/tbr/` — authoritative outer-loop state (TARGET/BEHAVE/REMEMBER)
- `.tbrpwn/pwn/` — inner-loop working state (Level1/2/3 PLAN/WORK/NOTE)
- `.tbrpwn/LOG.md` — append-only outer-cycle log

## Reset

If you want to restart from scratch:
- Delete everything under `.tbrpwn/` and re-copy templates from `tbr/` and `pwn/`.
- Keep `.tbrpwn/LOG.md` if you want an audit trail; otherwise delete it too.
