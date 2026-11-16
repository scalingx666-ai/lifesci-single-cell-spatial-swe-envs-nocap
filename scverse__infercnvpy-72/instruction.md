# Issue

**Title:** allow heatmap to use user's dendrogram

## Description

As mentioned in issue #71 the heatmap function doesn't allow to pass a custom dendrogram. Adding `uns` to the temporary AnnData object should fix this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0205938e825`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.