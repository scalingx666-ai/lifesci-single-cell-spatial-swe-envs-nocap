# Issue

**Title:** Assay argument in FeaturePlot

## Description

Addresses #10268 

The change is pretty straightforward, just passing the `assay` argument to `FetchData`

Example usage:

```{r}
library(Seurat)
library(SeuratData)
cbmc <- LoadData("cbmc")

cbmc <- NormalizeData(cbmc)
cbmc <- FindVariableFeatures(cbmc, selection.method = "vst", nfeatures = 2000, verbose = FALSE)

cbmc <- ScaleData(cbmc, features = VariableFeatures(cbmc), verbose = FALSE)
cbmc <- RunPCA(cbmc, features = VariableFeatures(cbmc), npcs = 30, verbose = FALSE)

cbmc <- RunUMAP(cbmc, dims = 1:30, reduction = "pca", verbose = FALSE)

# old behavior:
FeaturePlot(cbmc, "CD3D")
FeaturePlot(cbmc, "CD3") # plots CD3 from ADT assay with a warning

# new behavior:
FeaturePlot(cbmc, "CD3", assay="ADT") # plots CD3 from ADT assay without a warning
FeaturePlot(cbmc, "CD3D", assay="ADT") # plots CD3 from RNA assay with a warning
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31fb1430c141`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.