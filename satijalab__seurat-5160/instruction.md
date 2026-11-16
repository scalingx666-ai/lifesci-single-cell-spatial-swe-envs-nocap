# Issue

**Title:** Wrap examples/tests that use suggested packages in namespace guards

## Description

Includes:
- example for `BuildClusterTree` (requires `ape`)
- test for `Read10X_Spatial` (requires `hdf5r`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `09af635deb2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.