# Issue

**Title:** Fix pts

## Description

Fix two bugs in finding fixed points.

- The function will raise an unexpected error when no fixed points are found.
- The parameters should be passed as keyword arguments, or it will cause the error (because the order is different).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c0aa136e9ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.