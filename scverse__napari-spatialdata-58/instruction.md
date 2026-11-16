# Issue

**Title:** Fixing private module imports

## Description

Replacing `napari_spatialdata._interactive import Interactive` with `from napari_spatialdata import Interactive`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d331ac972388`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.