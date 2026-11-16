# Issue

**Title:** Use `int32_t` and `int64_t` for 10x H5 writing function

## Description

Hi, @bnprks 
When I tried to use `BPCells::write_matrix_10x_hdf5` in `loupeR` from https://github.com/10XGenomics/loupeR , the program `louper.exe create --input=<h5file> --output=<cloupe file>` raised an error:
```
indices: cannot convert dataset to int64
```
When I change the original `uint32/64_t` to `int32/64_t` in "indices" and "indptr", the error is fixed. Maybe it would be better if the HDF5 files written by `BPCells` use data types more consistent with 10x's expected formats, to improve compatibility with downstream tools.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8719e5868ff0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.