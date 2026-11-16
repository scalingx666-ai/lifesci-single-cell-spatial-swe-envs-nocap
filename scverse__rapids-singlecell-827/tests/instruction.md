# Issue

**Title:** Embed UMAP graphs too large for the GPU from their upper triangle, 200 epochs above 10k cells

## Description

- graphs whose device COO would not fit are cut to their upper triangle on the host (if canonical and symmetric) and embedded with twice the epochs: same quality, half the memory
- n_epochs defaults to 200 for more than 10,000 cells, like scanpy and umap-learn

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58da5a7d4198`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.