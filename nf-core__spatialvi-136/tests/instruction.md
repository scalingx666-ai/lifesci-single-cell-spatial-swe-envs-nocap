# Issue

**Title:** Add missing visium hd file checks

## Description

- Check for `feature_slice.h5` for downstream visium hd input files.
- Replace `raw_feature_bc_matrix.h5` with `filtered_feature_bc_matrix.h5` as we read filtered data using `spatialdata_io`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4bd0e61b628`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.