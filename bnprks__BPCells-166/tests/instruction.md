# Issue

**Title:** [r][cpp]Add supports to write `IterableMatrix` to dense H5 dataset with AnnData format

## Description

Hi, @bnprks,

Since `BPCells` now supports to read dense matrix from `h5ad` file, I add `write_matrix_anndata_hdf5_dense()` to write an `IterableMatrix` into a dense H5 dataset with `AnnData` format. This feature may help when users want to store a result matrix after a series of transformations, and reuse it in downstream analysis.

The implemention levervages `H5DenseMatrixWriter` class with `write()` method to handle row major or column major matrices. The standalone `write_matrix_anndata_hdf5_dense()` should work well without breaking the orignial designs for sparse matrices. In other words, we leave the choices of calling this feature to users. On the other hand, users don't need to concern about whether the input matrix is sparse, the function will always write the matrix into a 2D H5 dataset.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3d3d3518774`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.