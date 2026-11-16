# Issue

**Title:** Fix ci: huggingface token and codecov

## Description

- add a HF TOKEN to avoid "too many requests" error
- use existing python version from the matrix to run codecov

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85d3e2790481`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.