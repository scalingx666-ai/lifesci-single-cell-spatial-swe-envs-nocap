# Issue

**Title:** feat: LoadAtera reads Azimuth cell annotations when available

## Description

Load Azimuth cell type annotations in LoadAtera

LoadAtera previously dropped the per-cell Azimuth annotations stored in Atera outputs. It now adds them to the object's metadata when they are available.

New internal helper .AteraReadCellAnnotations() reads the azimuth_* columns from obs in cell_feature_matrix.zarr.zip. They aren't in csc_cell_feature_matrix.zarr.zip, which is the file the counts reader uses. It returns NULL if the file or columns are missing.
ReadAtera gains an "annotations" output type, not included by default.
LoadAtera gains cell.annotations = TRUE. Annotations are added with AddMetaData, after the cell subsetting, so they are aligned by cell name. A dataset without annotations loads as before, with no warning.
Columns are enumerated from the zarr group rather than the AnnData column-order attribute, which omits azimuth_coarse and azimuth_fine.
NEWS.md updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18159e111ece`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.