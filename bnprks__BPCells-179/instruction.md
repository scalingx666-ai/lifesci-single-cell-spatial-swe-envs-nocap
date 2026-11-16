# Issue

**Title:** [r] Fix perf subsetting large concatenated matrices

## Description

The logic for subsetting rbind or cbind matrices was taking time O(length(selection)* # sub-matrices), which could be quite slow for large datasets. Now, rather than performing a linear search through the selection indices to find the indices in range for each sub-matrix, we just do a binary search which eliminates the performance issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90bfbfd16614`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.