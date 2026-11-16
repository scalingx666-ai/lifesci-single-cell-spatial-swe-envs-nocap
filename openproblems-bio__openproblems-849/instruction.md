# Issue

**Title:** Subsample large datasets for pydrmetrics

## Description

We don't need to compute co-ranking on the full dataset -- once it's embedded, we can just use a subsample.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4571a779a01b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.