# Issue

**Title:** Resync with DelayedArray 0.35.2

## Description

`nzindex()` got removed from **DelayedArray** 0.35.2 (BioC 3.22) after being deprecated in BioC 3.20 and defunct in BioC 3.21. The replacement is to use `SparseArray::nzwhich(x, arr.ind=TRUE)`.

Also use `nzvals()` instead of `nzdata()`. The latter is just a slot accessor that only works on COO_SparseArray objects while the former works on _any_ SparseArray derivative (i.e. COO_SparseArray and SVT_SparseArray objects). It even works on dgCMatrix objects from the **Matrix** package. Furthermore, `nzdata()` is not guaranteed to return the non-zero values in an order that is consistent with the index returned by `nzwhich()`, but `nzvals()` is. See `?nzwhich` in the **SparseArray** package.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ed9aa25628e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.