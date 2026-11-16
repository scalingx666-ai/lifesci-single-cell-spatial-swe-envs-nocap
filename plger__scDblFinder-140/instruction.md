# Issue

**Title:** Pass on `nthreads` to `xgboost` functions in `scDblFinder`

## Description

We recently had some cases where `scDblFinder()` would grab all the cores on the machine, and run very slowly. Passing the `nthreads` parameter to the `xgboost` functions (which I believe would otherwise resort to `parallel::detectCores()`) seems to improve the situation and it finishes quickly (although as far as I can see it still uses a bit more CPU than specified via `BPPARAM`). The code below was enough to trigger the issue (both with versions 1.24.10 and 1.25.4):

```
library(scDblFinder)
library(SingleCellExperiment)
sce <- mockDoubletSCE(ncells = c(2000, 3000, 5000), ngenes = 10000)
sce <- scDblFinder(sce, BPPARAM=BiocParallel::SerialParam())
```

Is this something that you have also run into?

cc @mbstadler

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d322414bb07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.