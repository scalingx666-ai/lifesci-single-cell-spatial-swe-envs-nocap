# Issue

**Title:** Optimize `LeverageScore` for small BPCells inputs

## Description

Huge thanks to @yuhanH for this update 🚀 

---

Optimize the LeverageScore computation to address the long processing time for small BPCell matrices (fewer than 7,500 cells). Convert the input into a sparse matrix and then compute accurate leverage scores.  

In the current implementation, sketching pbmc3k takes approximately 100 seconds. With sparse conversion, this time is reduced to 30 seconds. For larger datasets like hcabm40k, the computation remains at 40 seconds.

```
library(Seurat)
library(SeuratData)
library(BPCells) 
data('pbmc3k')
data('hcabm40k')
 

obj <- UpdateSeuratObject(pbmc3k)
# obj <- UpdateSeuratObject(hcabm40k)

obj[['RNA']] <- as(obj[['RNA']], Class = 'Assay5')
obj[['RNA']]$counts <- write_matrix_dir(obj[['RNA']]$counts, dir = '~/test/pbmc3k_BPCells', overwrite = T)
obj <- NormalizeData(obj)
obj <- FindVariableFeatures(obj)
 
system.time(obj <- SketchData(obj))

```

---

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `179b877a2a58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.