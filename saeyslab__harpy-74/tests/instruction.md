# Issue

**Title:** SC_37 bump spatialdata

## Description

- bump spatialdata was causing issues due to `from datatree import DataTree` was no longer available. Replaced with `from xarray import DataTree`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6dfee9d9146`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.