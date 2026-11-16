# Issue

**Title:** Improved support for HDF5 transfer

## Description

. When converting from AnnData to SCE, if the former has HDF5-backed matrices, these automatically cause the creation of `HDF5Array`s (but only when those backed matrices are opened with `mode="r"`). This avoids any need to load the data into memory prior to the transfer into R.

In addition, there is some slightly better support for the reverse process. I couldn't figure out how to get the `AnnData()` constructor to accept a `h5py.Dataset`, but I did load the HDF5 file's contents into a Numpy array directly in Python; this avoids the need to load it in R before transferring to Python and saves a copy.

(Ideally, though, we would have AnnData accept a backed Dataset, as this is the direct analogue for a `HDF5Array`.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `724ecaab4994`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.