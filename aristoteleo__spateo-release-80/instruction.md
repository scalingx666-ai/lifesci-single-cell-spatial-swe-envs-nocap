# Issue

**Title:** Refine code on clustering

## Description

move normalization and dimension-reduction procedure out from scc function. Add function argument for pca_key to avoid key errors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55c7281e90ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.