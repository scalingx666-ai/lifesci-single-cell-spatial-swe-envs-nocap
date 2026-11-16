# Issue

**Title:** Rank-based Sampling and Setting Number of non-zero Cell and Neighborhood Tokens

## Description

In `CellNeighborhoodDataset`:

- Adds backwards compatible feature to `__getitem__` to collect gene tokens for cell and neighborhood based on log-normalised count based rank sampling strategy if strategy is specified. Otherwise, returns tokens unto specified sequence lengths.
- Adds feature to `__getitem__` to return the number of nonzero tokens corresponding to whether only cell, only neighborhood, or both tokens are used and if `cls` is included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1cba6de83adf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.