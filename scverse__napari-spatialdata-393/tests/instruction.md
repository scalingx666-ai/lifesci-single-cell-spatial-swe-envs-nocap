# Issue

**Title:** Support 3D visualization for points and 2.5D shapes

## Description

.

Builds on #366 to complete 3D support for vector data:

- 2.5D circles rendered at correct z depth
- Affine transforms respect z axis on coordinate system switch
- Save round-trip no longer drops z from points/shapes
- UI toggles for 3D points and 2.5D shapes projection
- Z-range slider to filter by depth

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88edca3fb841`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.