# Issue

**Title:** Transition to `poetry` + address `numpy 2.0` and `numba 0.60` related issues

## Description

... because numba fails the function signature check in Py 3.11

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a52b33dbd5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.