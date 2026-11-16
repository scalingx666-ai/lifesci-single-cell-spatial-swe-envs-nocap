# Issue

**Title:** add fixes for updatePairs, and Seurat variance scaling

## Description

Related to this issue: 

There are two fixes here: 
(1) I noticed that `sccore::plapply()` would give different results here: https://github.com/kharchenkolab/conos/blob/master/R/conclass.R#L1067-L1081

It looks like `pbmcapply::pbmclapply()` would result in a list with two elements, `$value` and `$warning`. Somehow, the warning output `Seurat doesn't support variance scaling` would become an element to the list....that was the fundamental error that the OP of the Issue #101 noticed. 

(2) Seurat has variance scaling now: https://satijalab.org/seurat/archive/v3.0/pbmc3k_tutorial.html
So I removed the warning, and applied this function.


If the PR is accepted, I'll update the CHANGELOG.

Background:

This code worked: 

```
library(Seurat)
suppressWarnings(library(SeuratData))
library(SeuratWrappers)
library(dplyr)
library(conos)
data("ifnb")

ifnb.panel <- SplitObject(ifnb, split.by = "stim")
for (i in 1:length(ifnb.panel)) {
  ifnb.panel[[i]] <- NormalizeData(ifnb.panel[[i]]) %>% FindVariableFeatures() %>% ScaleData() %>% 
    RunPCA(verbose = FALSE)
}

ifnb.con <- Conos$new(ifnb.panel)
ifnb.con$buildGraph(k = 15, k.self = 5, space = "PCA", ncomps = 30, n.odgenes = 2000, matching.method = "mNN", 
                    metric = "angular", score.component.variance = TRUE, verbose = TRUE)
```

This did not:
```
library(Seurat)
library(SeuratData)
library(conos)
LoadData("ifnb")

# split the dataset into a list of two seurat objects (stim and CTRL)
ifnb.list <- SplitObject(ifnb, split.by = "stim")

for (i in 1:length(ifnb.list)) {
    ifnb.list[[i]] <- NormalizeData(ifnb.list[[i]]) %>% FindVariableFeatures() %>% ScaleData() %>% RunPCA(verbose = FALSE)
}

con <- Conos$new(ifnb.list , n.cores=4)
con$buildGraph(k=15, k.self=5, space="PCA", ncomps=30, n.odgenes=2000, matching.method="mNN", metric="angular", 
      score.component.variance=TRUE, verbose=TRUE)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac09f5bd8c26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.