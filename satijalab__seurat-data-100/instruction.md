# Issue

**Title:** Fix package metadata

## Description

This PR makes some adjustments to the R package metadata for `SeuratData` to ensure it can be properly built & installed:

- Adds `importFrom` statements for `SeuratObject::Assays`, `methods::as`, and `methods::slot`
- Drops [this](https://github.com/satijalab/seurat-data/blob/4dc08e022f51c324bc7bf785b1b5771d2742701d/R/seurat_data.R#L183) reference to `Seurat.options` from `LoadData` 
- Explicitly lists `Seurat`, `Matrix`, and `methods` as package dependencies under "Imports"
- Updates the `.Rbuildignore` file to exclude the `.git/` folder during package build

Relates to:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4dc08e022f51`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.