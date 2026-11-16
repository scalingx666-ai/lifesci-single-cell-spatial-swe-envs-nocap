# Issue

**Title:** xarray bump

## Description

Sopa can not be installed with new xarray version xarray 2024.11.0 (due to from `datatree import DataTree` no longer working). Because of this it can also not be installed with new version of spatialdata 0.2.6. This is small PR to fix these issues.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f1f5a99ee7f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.