# Issue

**Title:** Do not save the cache column in the transcript patches to allow moving the `.zarr` directory before segmentation

## Description

Until now, we have saved the transcript patches location (absolute path) as a column in the corresponding GeoDataFrame.

The idea behind this is to be able to retrieve the cache even if a user does the following: running sopa in-memory until making the transcript patches, then saving the data on disk, and then running segmentation. **[Use case 1]**

But it was failing if the user did the following: saving the SpatialData object on disk, making the transcript patches, moving the SpatialData .zarr to another location, and then running segmentation. **[Use case 2]**

Both cases should be extremely rare, but case 2 is happening when running `nf-core/sopa` on AWS Batch, because the working directory changes.

This PR fixes **[Use case 2]** while breaking **[Use case 1]**. The rationale is that, if **[Use case 1]** happens (which is supposed to happen very rarely), then we have a meaningful error message explaining to just re-run the transcript patches. I think this is acceptable.

What do you think @kweisscure51?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `36eb2a812b8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.