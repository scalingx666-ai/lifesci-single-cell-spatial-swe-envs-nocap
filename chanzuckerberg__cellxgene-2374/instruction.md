# Issue

**Title:** undoable TS typing

## Description

Partial solution to #2366.  Adds typing to undoable-related reducer, configuration and state machinery.

Note that there are still two eslint disables in this PR, which await typing of the selection reducer state.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `925b785b1fa6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.