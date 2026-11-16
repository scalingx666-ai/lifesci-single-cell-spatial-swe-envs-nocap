# Issue

**Title:** Fleshed out writing tests

## Description

Turns out that `writeH5AD` + `readH5AD` coerces character vectors to factors. I wonder if there's a way to turn this off, it's another roadblock to a perfect round-trip.

Being able to remember the original name of the `X` matrix would also be kind of nice, but I guess there's not much choice there.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3dc45fafcfc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.