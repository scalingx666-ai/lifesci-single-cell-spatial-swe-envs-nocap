# Issue

**Title:** Updates to RunHarmony for compatibility with Seurat v5

## Description

Some fixes to `RunHarmony.Seurat` to retain compatibility with the upcoming Seurat v5 (`feat/standard` on [seurat-object](https://github.com/mojaveazure/seurat-object/tree/feat/standard)); mainly:
- Associates harmony's dimensional reduction with the assay from the input dimensional reduction
- Pulls grouping meta data for only the cells present in the input dimensional reduction

Also includes the additional improvements:
- Perform namespace check for Seurat and fail gracefully if not present
- Use Seurat's `Key` function (introduced in Seurat v4.1.1) to create keys for harmony's dimensional reduction
- Use `Seurat::Reductions` to find dimensional reduction objects in a `Seurat` object
- Move {SingleCellExperiment} to `Suggests` for easier installation of {harmony}

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea48a6c3c67f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.