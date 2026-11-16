# Issue

**Title:** Add soft constraints to the model for semi-supervision of cell probabilities

## Description

For the droplets that are "surely cells" or "surely empties", use a soft constraint to ensure that the cell probability encoder does not get off-track.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cab2ff167bc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.