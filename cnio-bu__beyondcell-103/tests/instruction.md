# Issue

**Title:** BC2_RC0

## Description

Merging the first candidate back to developing as too many changes were incorporated to the branch. This PR enables the CI for pushes and PRs to both master an developing, updates the conda recipe and update/trim the required dependencies for beyondcell.

We also got rid for umap-learn, once and for all-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f48447336c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.