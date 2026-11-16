# Issue

**Title:** Adding assay parameter to generate_cytospace_from_scRNA_seurat_object

## Description

Adding a `rna_assay` parameter with default to `RNA` since `GetAssayData` by default grabs current `DefaultAssay` if no `assay` is provided.
Without this, could cause some issues such as count matrix in the `SCT` instead of `RNA` assay is used. Or in my case, in a multiome object (snRNA/ATAC), the Peak accessibility of snATAC assay was set as Default Assay due to other previous operations on the Seurat object. The chromosome accessibility was extracted instead of RNA expression count. 
Hope this makes sense!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5654a6a6b659`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.