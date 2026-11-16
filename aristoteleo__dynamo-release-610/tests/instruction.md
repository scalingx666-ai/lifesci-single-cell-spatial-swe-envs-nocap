# Issue

**Title:** Debug uniform indices sampling in fate()

## Description

Bug description: The structure of uniform indices doesn't support multiprocessing. Also, the output shape is not consistent with other methods.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `199d9b995a42`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.