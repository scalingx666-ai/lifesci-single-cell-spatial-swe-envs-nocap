# Issue

**Title:** Debug _cosmx_morphology_coords when one or more morphology channels are unused

## Description

When one or more morphology channels has no biological target, returns those channels' single-letter names to the morphology coordinates. This prevents an error caused by mismatching dimensions with the shape of the TIF dask array, which always includes all 5 channels.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `69499a2b3bd4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.