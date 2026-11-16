# Issue

**Title:** Add alpha size vis

## Description

Hey @ncborcherding,

I wanted to change the `size` and `alpha` parameter of the `DimPlot` in the `clonalOverlay` plot because of overplotting.
I found no easy solution to change these parameter post plotting (e.g. manipulating `umap_plot[[1]]$layers[[1]]@aes_params$alpha` works in `Seurat::DimPlot` but not here).
So this is just a simple change to expose these two parameters to the users.

Best,
Mischko

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `52a0738c5fa1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.