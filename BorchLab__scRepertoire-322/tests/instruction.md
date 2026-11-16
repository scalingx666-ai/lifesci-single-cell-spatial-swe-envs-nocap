# Issue

**Title:** Allow selecting a single diversity metric in 'clonalDiversity()'

## Description

This PR fix a simple bug to allow users to select and show a single diversity metric in `clonalDiversity()`

```r
Error in mat[, group.by] <- names(input.data): incorrect number of subscripts on matrix
Traceback:

1. clonalDiversity(combined.TCR, cloneCall = "gene", chain = "both", metrics = "shannon")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a919b93e308`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.