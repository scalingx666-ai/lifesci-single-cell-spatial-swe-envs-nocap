# Issue

**Title:** Support Baysor>=7.0.0

## Description

Hi @lguerard, I added a test to check if the cell IDs are string
In the new 0.7.0 version, the cell IDs are strings, and we need to use the obs_names instead of CellID to compare to the loom matrix

Let me know if this works for you!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7feb2d3ef42d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.