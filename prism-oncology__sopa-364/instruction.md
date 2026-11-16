# Issue

**Title:** Ensure 2d transformations are always used for shapes

## Description

Solve an issue when:
1. Using 3D points with an Affine transformation
2. Then saving on disk
3. Then running segmentation

Afterwards, it creates a weird `(x, y) -> (z, x, y)` transformation that can't be used. This issue solve this (a fix in SpatialData directly may be considered)

Related SpatialData issue:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f393f8f39f66`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.