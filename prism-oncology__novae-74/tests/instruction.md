# Issue

**Title:** Add cell sampling in kmeans when re-updating prototypes

## Description

Also, minor refactoring:
- Rename internal variable `sampling_size`
- Rename some internal `Keys` names

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4c061e1f855`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.