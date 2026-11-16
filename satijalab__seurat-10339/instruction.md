# Issue

**Title:** Fix #10332 by updating object creation step in `as.Seurat.SingleCellExperiment`

## Description

The `as.Seurat.SingleCellExperiment` conversion function checks whether a variable named object already exists before creating a new Seurat object, using `exists("object")`. `exists` checks within the global environment as well, meaning that if `object` already exists in the R session, the function behaves as though the Seurat object is already initialized, skipping to setting assay data. Then, if the existing object and incoming data have different dimensions, this results in an error about replacement length mismatch. Reprex below.

``` r
# replace with path to repo on the main branch
main_branch_path <- "~/seurat"
devtools::load_all(main_branch_path, quiet = TRUE)
suppressPackageStartupMessages(library(SeuratData))
print(git2r::repository_head(repo = main_branch_path)) # verify repo on main
#> [3f6462] (Local) (HEAD) main

suppressWarnings({suppressMessages({
  obj <- LoadData("pbmcsca")
  obj <- subset(obj, nFeature_RNA > 1000)
  obj[["RNA"]] <- split(obj[["RNA"]], f = obj$Method)
  
  obj <- NormalizeData(obj)
  obj <- FindVariableFeatures(obj)
  obj <- ScaleData(obj)
  obj <- RunPCA(obj)
  
  obj <- obj %>% JoinLayers() %>% as.SingleCellExperiment() 
})})

try1 <- as.Seurat(obj) # successful
object <- obj
try2 <- as.Seurat(object) # errors
#> Error in `[[<-`(`*tmp*`, i, ..., value = value): 33694 elements in value to replace 10434 elements

# replace with path to repo pointing to fix/sce-as-seurat branch
fix_branch_path <- "~/seurat-testing-clone/seurat"
devtools::load_all(fix_branch_path, quiet = TRUE)
suppressPackageStartupMessages(library(SeuratData))
print(git2r::repository_head(repo = fix_branch_path)) # verify repo on fix
#> [8e5dc3] (Local) (HEAD) fix/sce-as-seurat

try1 <- as.Seurat(obj) # successful
try2 <- as.Seurat(object) # successful
```

<sup>Created on 2026-03-19 with [reprex v2.1.1](https://reprex.tidyverse.org)</sup>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f6462bbdc4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.