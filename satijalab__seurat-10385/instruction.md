# Issue

**Title:** Fix `FindClusters` behavior when passed a vector of resolutions and custom names

## Description

# Summary
`FindClusters` was no longer assigning cluster-associated metadata properly when passed a vector of resolutions and custom cluster names - the active identity was being assigned using `cluster.name` (containing all custom cluster names) instead of `idents.use`. Here, `idents.use` is the name of the last clustering column that was created in clustering.results, ensuring the active identity is properly updated for the most recent clustering run. In this fix, we switch to using this for active identity assignment for custom cluster names. (Note that the individual resolution columns were already correctly stored earlier via `object[[]] <- clustering.results`.)

In addition to fixing this bug, this PR also proposes two tests in `tests/testthat/test_find_clusters.R`, checking that:
1. `FindClusters` works if passed a vector of resolutions
2. `FindClusters` sorts numeric factor levels correctly (the bug in question was initially introduced in the process of fixing the level ordering issue)

## Type of change
Bug fix (non-breaking change fixing an issue)

## Tests & examples

`test_find_clusters.R` includes a test for this fix, below is a reproducible example adapted from #10382.

```r
# first check out this branch
devtools::load_all(".")
library(SeuratData)
library(dplyr)
pbmc <- LoadData("pbmc3k")

pbmc <- NormalizeData(pbmc) %>% FindVariableFeatures() %>% ScaleData() %>% RunPCA(features = VariableFeatures(pbmc)) %>% FindNeighbors(dims = 1:10)
res_sequence <- seq(0.4,0.8, by = 0.1)

pbmc <- FindClusters(pbmc, resolution = res_sequence, cluster.name = paste0("resolution_",res_sequence))

for (i in res_sequence) {
  col_name <- grep(i, colnames(pbmc@meta.data), value = TRUE)
  print(unique(pbmc@meta.data[[col_name]]))
}
```

## Related issues


## Checklist

- [x] Branch is named appropriately (`feat/*`, `fix/*`, `docs/*`)
- [x] Code follows Seurat [style guidelines](https://github.com/satijalab/seurat/wiki/Contributor%27s-Guide)
- [x] Documentation and comments have been updated
- [x] `devtools::document()` has been run
- [x] `devtools::check()` passes with no errors or warnings
- [x] Test case demonstrating new functionality is included

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `053380e7697d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.