# Issue

**Title:** Fix GetResidual() for multi-model SCT assays

## Description

This PR fixes GetResidual() behaviour for SCT assays that contain multiple SCT models that resulted from separate runs of SCTransform(). 

Previously, GetResidual() behaved incorrectly when requested features were not modeled in every SCT model in a Seurat object; when its parameter na.rm was set to FALSE, this should normally remove all genes with NAs from the residual matrix. However, without these changes, this would instead result in a crash with the following error: `# Error: number of rows of matrices must match (see arg 2)`. 

Reproducible example (thank you @pwwang!): 
```
library(Seurat)
data("pbmc_small", package = "SeuratObject")
set.seed(1)
obj1 <- SCTransform(pbmc_small[, 1:40], verbose = FALSE)
obj2 <- SCTransform(pbmc_small[, 41:80], verbose = FALSE)
merged <- merge(obj1, obj2)

# a gene modeled in obj1 only, and one modeled in both objects
only1 <- setdiff(VariableFeatures(obj1), VariableFeatures(obj2))[1]  # e.g. "TCL1A"
both  <- intersect(VariableFeatures(obj1), VariableFeatures(obj2))[1]

# na.rm = FALSE: crashes
GetResidual(merged, features = c(only1, both), assay = "SCT", na.rm = FALSE)
# Error: number of rows of matrices must match (see arg 2)
```

This PR introduces some changes to GetResidual(), GetResidualSCTModel(), and FetchResidualSCTModel() that addresses these issues. 

GetResidual() is normally supposed to loop over each SCT model in an object and call the GetResidual/FetchResidual helpers to recompute any missing residuals. However the previous code just passed the object's entire set of cells, making the output structurally inconsistent. GetResiduals() now passes the current model's cells into the residual calculator helpers, such that each SCT model correctly computes residuals for its own cells.

GetResidualSCTModel() and FetchResidualSCTModel() now explicitly handle partial feature overlap better by only computing residuals for features present in a model, and padding any missing features with NAs. 

With these changes, the residual matrix for the above reprex now generates correctly:
```
#Print residuals for 4 cells, of which 2 cells lack the TCL1A feature in their SCT model
> residual_mat[c(only1, both), 39:42]
      GGCATATGCTTATC CATTACACCAACTG TAGGGACTGAACTC GCTCCATGAGAAGT
TCL1A     -0.2626143      -0.325272             NA             NA
GNLY       1.3417045       1.341705       1.302976     -0.1981292
```

Simple example of the problem: 
Suppose GetResidual is called for features **A** and **B** across an SCT assay with two SCT models. model1 contains both A and B, but model2 contains only B. model1 contains cells c1, c2, while model2 contains cells c3, c4. Under healthy GetResidual na.rm = FALSE behaviour, we would expect the residual matrix to look something like:

```text
      c1   c2   c3   c4
A    0.2  0.1   NA   NA
B    0.1  0.2  0.3  0.1
```
Without these changes, running Get/FetchResidualSCTModel would return

```text
      c1   c2
A    0.2  0.1
B    0.1 0.2
```

for model1 and

```text
      c3   c4
B    0.3 0.1
```
for model two, with inconsistent row sets that cause GetResidual to error. After this change, each model computes residuals only for the features it contains, however the helper functions now also pad missing features with NA:

```text
      c1   c2
A    0.2  0.1
B    0.1  0.2
```
for model1 and 

```text
      c3  c4
A    NA  NA
B    0.3  0.1
```
for model 2. This would eventually combine into the full residual matrix that can now be returned by GetResidual():

```text
      c1   c2   c3   c4
A    0.2  0.1   NA   NA
B    0.1  0.2  0.3 0.1
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9015bf82bb5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.