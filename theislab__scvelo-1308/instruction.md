# Issue

**Title:** Implement fix of get_sparse_from_igraph() theislab/scvelo#1241

## Description

## Bug fixes

-   Fixes bug that results in `ValueError: mismatching number of index arrays for shape; got 0, expected 2` when running `scv.tl.paga`


## Related issues

<!-- Please list related issues. If none exist, open one and reference it here. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f89590b5912f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.