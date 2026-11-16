# Issue

**Title:** Extend doublet_weight param in doubtletFromCellType()

## Description

- Can accept either a float or sequence of floats for weights of each
parent cell type. A single float will be used for both weights.

Also set both synth doublet generators follow data type of original
data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5df7363530ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.