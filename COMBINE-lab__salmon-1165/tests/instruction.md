# Issue

**Title:** fix(group 3): detect incompatible flag combinations at invocation

## Description

**Group 3 of 4** (#1140). Each of these is fully known from the command line, and each was previously resolved by silently discarding one side. Stacked on #1164.

| Combination | Was | Now |
|---|---|---|
| `--annotation` without `-a` | Whole genome-projection request dropped silently; paths never even checked for existence | Errors, naming both flags |
| `--errorModel` + `--noErrorModel` | Silent precedence (`--noErrorModel` won) — then salmon advised passing `--errorModel`, already on the command line | clap conflict |
| `--skipQuant` + `--numBootstraps`/`--numGibbsSamples` | Discarded in silence, while sibling `--dumpEq` and `-g` both explain themselves | Warns, naming the recovery (quantify the kept RAD with `--rad`) |
| `--thinningFactor` without `--numGibbsSamples` | Silently inert; the analogous `--bamCompressThreads` without `--writeBam` already errors | Option-typed and warned |

## Worth knowing: `requires` was not enough

My first attempt at `--annotation` used clap's `requires = "alignments"` alone. It doesn't fire for the cases that matter: **clap skips a `requires` when the required argument conflicts with one already present**, and `-1/-2`, `-r` and `--rad` all conflict with `-a`. Those are exactly how a user reaches this mistake, so all three sailed through.

The `requires` is kept (it covers the no-other-input case and chains correctly from `--genome`), but the real enforcement is an explicit check. That check also had to move: my first placement sat inside the reads branch and missed `--rad`, which the test caught — the `--rad` branch dispatches earlier. It now runs before mode dispatch, alongside the other invocation-time validations.

Both facts are recorded in comments at the site, since the next person to add a `requires` in this file will hit the same thing.

Suite **331/0**, clippy clean. Group 4 next; Group 5 tracked in #1162.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a396dc2b3b25`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.