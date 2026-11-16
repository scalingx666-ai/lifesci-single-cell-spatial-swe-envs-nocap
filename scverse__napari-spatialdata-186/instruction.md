# Issue

**Title:** remove npe related parts

## Description

This PR resolves the comment of @psobolewskiPhD in #185. Specifically it removes those parts of the code related to `npe` and adds instructions in the readme to allow users to use `napari-spatialdata` as the default `.zarr` extension reader.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f7f5d663cf5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.