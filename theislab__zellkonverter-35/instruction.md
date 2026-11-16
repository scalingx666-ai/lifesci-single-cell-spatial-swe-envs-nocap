# Issue

**Title:** Write DelayedArray to file on the R side.

## Description

. 

```r
library(zellkonverter)
library(scRNAseq)
sce <- ZeiselBrainData()
counts(sce) <- DelayedArray(counts(sce))
 
temp <- tempfile(fileext = ".h5ad")
writeH5AD(sce, temp)
```

Some points:

- Need to test that it works with both DA in the first and/or later assays.
- Need to test that the result is still readable by `readH5AD`.

Known to-dos:

- The code does not respect `is_sparse()` being `TRUE`. A little bit of work is required to achieve a one-pass writer that does not rely on knowing the total number of non-zero entries.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec62688686c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.