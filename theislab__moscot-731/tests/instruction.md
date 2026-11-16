# Issue

**Title:** Introduce a `groupby` attribute for correlation computation

## Description

This introduces a `groupby` parameter for `mapping_problem.correlate()` to evaluate Pearson/Spearmann correlation over groups of cells. I've also adapted tests slightly to cover this case.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3fd4544b6aa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.