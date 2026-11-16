# Issue

**Title:** Fix 'ident' field name of sc object in '.grabMeta()'

## Description

This PR fix a simple bug in `.grabMeta()`. 
When the input is a `SingleCellExperiment`, the corresponding `ident` field in `colData` should be `label`. The fix should allow the correct selection of the column containing cell cluster labels.

```r
ERROR while rich displaying an object: Error in `geom_point()`:
! Problem while computing aesthetics.
ℹ Error occurred in the 1st layer.
Caused by error in `[.data.frame`:
! undefined columns selected
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a919b93e308`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.