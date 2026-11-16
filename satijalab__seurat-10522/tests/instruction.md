# Issue

**Title:** Fix SCTransform for BPCells assay layers

## Description

Fixes a regression where `SCTransform` on BPCells assay layers fails when `ncells` is smaller than the layer’s cell count. This also affects default settings for assays with more than 5,000 cells. Separately, disabling UMI correction or using a reference SCT model fails when assigning BPCells data to the output assay.

Restore the previous assay workflow and preserve output for all cells by converting `IterableMatrix` layers to sparse matrices before SCT processing (this is the behavior present in previous versions). This avoids creating an intermediate assay and leaves other input types and direct `IterableMatrix` calls unchanged.

Small example:

```r
library(Seurat)
library(BPCells)

counts <- GetAssayData(pbmc_small, assay = "RNA", layer = "counts")
obj <- CreateSeuratObject(
  counts = CreateAssay5Object(counts = as(counts, "IterableMatrix"))
)
reference <- SCTransform(pbmc_small, verbose = FALSE)[["SCT"]]@SCTModel.list[[1]]

results <- list(
  sampled = SCTransform(obj, ncells = 20, verbose = FALSE),
  uncorrected = SCTransform(obj, do.correct.umi = FALSE, verbose = FALSE),
  reference = SCTransform(obj, reference.SCT.model = reference, verbose = FALSE)
)
# on main this fails with "Error in `LayerData<-` at seurat-rewrite/R/preprocessing5.R:1442:3:
# ! The new data must have the same number of cells as the current data"
for (result in results) {
  residuals <- LayerData(result[["SCT"]], layer = "scale.data")
  stopifnot(
    ncol(result[["SCT"]]) == ncol(obj),
    setequal(colnames(residuals), colnames(obj)),
    !anyNA(residuals)
  )
}
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `46ab1a471781`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.