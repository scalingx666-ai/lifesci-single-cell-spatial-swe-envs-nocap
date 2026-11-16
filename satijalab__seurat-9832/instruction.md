# Issue

**Title:** Fix `FindTransferAnchors` to support multi-layer query

## Description

This PR enables running `FindTransferAnchors` using a `query` containing more than one layer. Since `FindTransferAnchors` is the main function underpinning `Azimuth::RunAzimuth`, this change will also mean that the latter function works with multi-layer queries too. 

When the `mapping.score.k` parameter is set, "query.neighbors" are cached for later use by the `MappingScore` method. In the multi-layer case, these query neighbors need to be calculated and cached layer by layer.  

This PR also adjusts `MappingScore` to potentially expect a _list_ of precomputed `Neighbor` objects, one for each layer. The output of `MappingScore` isn't affected since there is still just one score per query cell. 

You can verify the fix with the following snippet:

```r
library(Seurat)
library(SeuratData)


query <- LoadData("ifnb")
query <- split(query, f = query$stim)
query <- NormalizeData(query)

reference <- LoadData("pbmc3k")
reference <- NormalizeData(reference)
reference <- FindVariableFeatures(reference)
reference <- ScaleData(reference)
reference <- RunPCA(reference)

transfer_anchors <- FindTransferAnchors(
  reference = reference,
  query = query,
  reference.reduction = "pca",
  mapping.score.k = 100
)
```

And the same for `Azimuth`:

```r
library(Seurat)
library(SeuratData)
library(Azimuth)


ifnb <- LoadData("ifnb")
ifnb <- split(ifnb, f = ifnb$stim)

RunAzimuth(ifnb, reference = "pbmcref")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9fee80a70863`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.