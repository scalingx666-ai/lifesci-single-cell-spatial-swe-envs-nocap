# Issue

**Title:** Use Seurat's object creation and data setter functions

## Description

`ligerToSeurat` was creating `DimReduc` objects using `new` instead of `CreateDimReducObject`; this caused issues where the `DimReduc` object was incomplete due to lack of embedding names and empty slots (see satijalab/seurat#3574).

This PR uses `Seurat::CreateDimReduc` object (called using the `::` construct to avoid importing and depending on Seurat) to create dimensional reduction objects to ensure the `DimReduc` objects are complete. In addition, it uses `[[<-` to add the dimensional reduction information to ensure that all `DimReducs` go through proper validation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c8b7c6ecff7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.