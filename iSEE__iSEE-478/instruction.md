# Issue

**Title:** Rolled out slot updaters to a dedicated function.

## Description

We need to double-check that all new slots are covered by the updaters.

We also need to stick `updateObject()` calls in `[[` and `[[<-`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7df4c927310d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.