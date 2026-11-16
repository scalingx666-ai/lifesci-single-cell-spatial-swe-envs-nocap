# Issue

**Title:** Dev 4.1

## Description

- Pseudocount option (no breaking change), but when set to 1, sparse operations can be applied on matrix so it never becomes dense
- Updated notebook to clarify this
- PCA solver set to a faster one for dense matrices (technically a breaking change but results are within stochasticity of method), the breaking change technically came from scanpy a few versions ago as they changed their default solver.
- Method is at least 50% faster with just changing the pca solver

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d25393d70db1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.