# Issue

**Title:** [r] Fix `knn_hnsw()` input query rowname bug

## Description

This pull request fixes a bug in `knn_hnsw()` where the rownames of the result matrices were incorrectly taken from `data` instead of `query` when a separate query matrix was provided. This caused the output to have wrong rownames (from the reference data) rather than the rownames corresponding to the actual query points. When no query is given, `query` is already set to `data`, so behavior is unchanged in that case. (`r/R/clustering.R`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c293a0a34e65`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.