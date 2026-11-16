# Issue

**Title:** Bump version: 1.3.0 → 1.3.1

## Description

Update a new patch for Dynamo ver 1.3

- Remove cdlib and KDEpy from the requirement.
- Add the sampling number n to the parameters of the topography plotting function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c92abbd6e0da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.