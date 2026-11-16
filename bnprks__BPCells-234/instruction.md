# Issue

**Title:** [cpp] add fix for `write_matrix_hdf5()` when overwriting nonexistent file

## Description

Pretty self explanatory.  Added a conditional to `hdf5_group_exists_cpp` to ensure we're not checking for a group in a file that doesn't exist.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa6443a764a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.