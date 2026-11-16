# Issue

**Title:** Fix dimplot fetch

## Description

This PR fixes a bug where DimPlot will pull columns from meta.data instead of using the embeddings from the reduction object, if the metadata contains columns named like a dimension - `'PC_1', 'UMAP_1'` etc. This .

```
library(Seurat)

DimPlot(pbmc_small, reduction = "pca") # works as expected

pbmc_small$PC_1 <- rep(1, ncol(pbmc_small)) # add meta column with PC_1 name

DimPlot(pbmc_small, reduction = "pca") # incorrectly uses meta.data$PC_1

```

This produces a nonsense plot, as the metadata column overrides the embedding.

Proposed Fix:

- Explicitly fetch embeddings from `Embeddings(object[[reduction]])`
- metadata is then appended separately
- This guarantees that dim reduction coordinates come from the reduction always

Test added:

- Unit test ensuring that if a metadata column collides with an embedding dimension name (`'PC_1', 'UMAP_1'`), DimPlot still uses the reduction embeddings
- The test fails on current main branch, but passes with the fix

Impact:

- Prevents name collisions between metadata and reduction dimensions
- Behaviour of existing code without collisions is unchanged

Checklist:

- [x]  Bug Fixed (#10061)
- [x]  Test Added
- [x]  Documentation updated with roxygen2

<!--
Thanks for your interest in contributing! 

Please refer the contributor's guide for instructions on submitting a pull request:
https://github.com/satijalab/seurat/wiki#contributors-guide
-->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `70a8b2716db1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.