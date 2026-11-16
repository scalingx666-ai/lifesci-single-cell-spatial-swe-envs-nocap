# Issue

**Title:** major revision of seq- chapter between QC & clustering

## Description

- clearer overall structure (1. norm, 2. selection, 3. dimred, 4. viz)
- reduced text redundancies
- mention of `SpaNorm`
- replace UMAP by PCA plot
- save only 1 object for simplicity

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b1b6e551bca2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.