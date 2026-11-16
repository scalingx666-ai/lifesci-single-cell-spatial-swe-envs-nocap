# Issue

**Title:** Fix Stardist+Proseg usage on Visium HD for recent anndata versions

## Description

We need to set `anndata.settings.allow_write_nullable_strings = False` before writing the bins-table for proseg else it doesn't detect the genes (due to pandas v3). This PR fixes that by using a context manager around the zarr writing.

@jluft-uoe, if you have time, could you please confirm that using this branch fixes your issue (without to manually set `anndata.settings.allow_write_nullable_strings = False` before running `sopa.segmentation.proseg`)?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `77bbba254bde`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.