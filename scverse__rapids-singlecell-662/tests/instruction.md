# Issue

**Title:** unify cublas handle creation

## Description

This will unify the cublas handle creation in harmony with GMM. This is also now the template for all upcoming cuBLAS calls

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7321cb4117dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.