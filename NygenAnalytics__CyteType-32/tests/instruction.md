# Issue

**Title:** Add sampling for visualization coordinates in CyteType

## Description

Introduces a helper function to sample a maximum number of cells per group for visualization, reducing memory usage and improving performance for large datasets. Updates CyteType to use this sampling logic and adds a max_cells_per_group parameter to control the sampling limit. Bumps version to 0.6.1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8cdd87e4f90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.