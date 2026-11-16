# Issue

**Title:** Fixes to var_by_distance functionalities

## Description

- Fixes `tl.var_by_distance()` behaviour if numpy arrays of coordinates are passed as anchor point.
- Updates `pl.var_by_distance()` to plot multiple variables on a single plot.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d3761f58de6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.