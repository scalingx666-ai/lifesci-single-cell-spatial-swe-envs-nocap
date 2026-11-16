# Issue

**Title:** Rename SpatialImage to VirtualSpatialImage class

## Description

This is to fix the current error in the `spatialLIBD` build report for version 1.7.12, which is due to the renaming of the `SpatialImage` class to `VirtualSpatialImage` in `SpatialExperiment` version 1.5.3.

`spatialLIBD::check_spe()` was using the old class name `SpatialImage` for a check, so this was returning an error in the vignette where this function is used. Renaming this to `VirtualSpatialImage` in `spatialLIBD::check_spe()` should fix it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a41643809cd8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.