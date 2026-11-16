# Issue

**Title:** Make sure cells.highlight is not dataframe

## Description

Example:


```r
library(Seurat)
DimPlot(pbmc_small, cells.highlight = pbmc_small[[]])
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4638730d063`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.