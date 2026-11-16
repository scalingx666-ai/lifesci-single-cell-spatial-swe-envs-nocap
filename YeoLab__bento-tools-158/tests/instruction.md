# Issue

**Title:** multimapping shapes

## Description

> Shapes are currently mapped "1 to 1" with _sjoin_shapes() and multiple shapes e.g. nuclei assigned to the same cell shape are dropped and only one is kept. The goal is to support "1 to many" mappings for cells. Some use cases include complex organelles like the ER, golgi, or those with multiple instances in the same cell e.g. condensates, granules, vesicles, or just arbitrary domains. #157 

- [ ] more robust shape indices

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b0ddc030ec68`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.