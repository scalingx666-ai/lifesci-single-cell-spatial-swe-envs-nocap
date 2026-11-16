# Issue

**Title:** Fixed some bugs in CCI code

## Description

Most of my changes are adding additional type checks for anndata object, since the obs_names could be numeric and adata.X could be a np.ndarray instead of a sparse array. 

There's also some changes for deprecated code, like it is not allowed to use set as a subscription on dataframes now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e8b8822e4ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.