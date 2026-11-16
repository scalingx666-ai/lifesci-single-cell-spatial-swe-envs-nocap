# Issue

**Title:** fix AttributeError: 'AnnData' object has no attribute '_get_X'

## Description

- Add a backward compatible fix to support `anndata 0.13` for #400
- Also bump the min Python to 3.12, and test also 3.13 and 3.14

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1150de77d9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.