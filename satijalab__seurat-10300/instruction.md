# Issue

**Title:** add vars.to.regress functionality to ScaleData.IterableMatrix

## Description

This is an enhancement for `ScaleData.IterableMatrix()` (for BPCells Seurat object) requested by multiple users (e.g., see ). 

- Description of the issue:
When performing `ScaleData()` to a regular Seurat object with dgcMatrix, users can specify `vars.to.regress` (or `latent.data`) to regress out covariates from the data matrix before scaling/centering. However, this was never implemented for `ScaleData.IterableMatrix`. 

- Enhancement: 
@bnprks has already implemented this regress_out functionality in `BPCells::regress_out()` (described here: ), so I updated `ScaleData.IterableMatrix()` to incorporate this change. 

- Reproducible codes:
I generate a standard object (dgcMatrix) and a BPCell object (IterableMatrix) below, together with some covariates to adjust for. With this PR, we should see identical adjusted matrices for the two objects.  
```
library(SeuratData)
library(BPCells)
devtools::load_all("~/github_repo/seurat/")

##  1. A standard dgcMatrix object
pbmc <- pbmc3k
pbmc <- UpdateSeuratObject(pbmc)

pbmc$var1 = rnorm(n = ncol(pbmc))
pbmc$var2 = rnorm(n = ncol(pbmc), sd = 2)
pbmc$cat1 = sample(x = c("A", "B"), size = ncol(pbmc), replace = T)
# need to create a covariate that is actually correlated with the data 
pbmc$cat2 = "CD4 T"
pbmc$cat2[pbmc$seurat_annotations == "Memory CD4 T"] = "Not CD4 T"

# 
pbmc = NormalizeData(pbmc)
pbmc = FindVariableFeatures(pbmc)
pbmc = ScaleData(pbmc, vars.to.regress = c("var1", "var2", "cat1", "cat2"))


##  2. Generate a BPCells object 
obj <- pbmc3k
obj <- UpdateSeuratObject(obj)

# write_matrix_dir(mat = obj[["RNA"]]$counts, dir = '~/BPCell_ct')

# 2. Open the directory as a BPCells matrix
counts.mat <- open_matrix_dir(dir = "~/BPCell_ct")

# 3. Replace the assay layer
obj[["RNA"]] <- CreateAssay5Object(counts = counts.mat)
obj <- AddMetaData(obj, metadata = pbmc@meta.data)

# 4. test the var.regress:
obj <- NormalizeData(obj)
VariableFeatures(obj) <- VariableFeatures(pbmc)
obj <- ScaleData(obj, vars.to.regress = c("var1", "var2", "cat1", "cat2"))

############################
##   compare the matrices to see if they match each other; should check through different genes 
############################

plot(x = pbmc[['RNA']]$scale.data["S100A9", ], 
     y = as.matrix(obj[['RNA']]$scale.data["S100A9", ]), 
     xlab = "dgcMatrix", 
     ylab = "BPCells")

abline(0, 1)

```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1693636c68cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.