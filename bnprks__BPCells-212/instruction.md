# Issue

**Title:** [r] add examples for matrix io functions

## Description

Pretty self explanatory, with the design choice logic from  I did add some horizontal breaks as discussed from our chat, for multiple functions in the same Rd. This should help with readability going forward.

For `write_matrix_anndata_hdf5()`, I had to put the example in the `open_matrix_anndata_hdf5()` docstring instead.  This is because I did not find an easy url to download an anndata h5 file, so writing one via `write_matrix_anndata_hdf5()` felt like a decent alternative.  I'm open to alternatives though.

I could not find any examples for `MatrixMarket` files that were reasonable in size, and we do not have a function to turn an `IterableMatrix` into one.  Any suggestions?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `647f9ee771d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.