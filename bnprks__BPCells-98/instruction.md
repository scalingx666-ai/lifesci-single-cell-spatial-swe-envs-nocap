# Issue

**Title:** fix setMethod not found when loading

## Description

When using BPCells in other package, R CMD Check report following errror:
![image](https://github.com/bnprks/BPCells/assets/19575010/3df5a649-363a-4c1e-9181-bdfddce166b1)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84e87448e71b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.