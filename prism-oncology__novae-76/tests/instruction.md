# Issue

**Title:** Speed-up data loader

## Description

For non-scConcept Novae models, the subset `adata[:, self._keep_var(adata)]` was performed for every `__getitem__`. Unexpectedly, this was very slow.

In this PR, I perform this operation once, during the init of the `ZScoreTorch` class. I also removed the unnecessary label encoder.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ee6d0c58083`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.