# Issue

**Title:** Fix PercentageFeatureSet to respect the `assay` parameter

## Description

This PR makes two small changes to `PercentageFeatureSet`:

1. Correctly passes `assay` to the `Layers` call on [line 1178 of utilities.R](https://github.com/satijalab/seurat/blob/9755c164d99828dbc5dd9c8364389766cd4ff7fd/R/utilities.R#L1178). 
2. Raises a warning when the `features` parameter contains values not present in the specified `assay` instead of erroring out.

My intent is to introduce a proper test for `PercentageFeatureSet`, but the following scripts can be used to verify the fixes for now. Verify that `assay` is being respected:

```R
library(testthat)
library(Seurat)

counts <- LayerData(pbmc_small, assay = "RNA", layer = "counts")
data <- LayerData(pbmc_small, assay = "RNA", layer = "data")

assay_left <- CreateAssay5Object(data = data)
assay_right <- CreateAssay5Object(counts)

test_case <- CreateSeuratObject(assay_left, assay = "LEFT")
test_case[["RIGHT"]] <- assay_right

DefaultAssay(test_case) <- "RIGHT"
expected <- PercentageFeatureSet(test_case, assay = "RIGHT", pattern = "^RP[LS]")

DefaultAssay(test_case) <- "LEFT"
result <- PercentageFeatureSet(test_case, assay = "RIGHT", pattern = "^RP[LS]")

expect_true(identical(result, expected))

```

And check that a warning (not an error) is raised when `features` contains values absent in the specified (default) assay:

```R
PercentageFeatureSet(pbmc_small, features = "not-a-gene")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9755c164d998`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.