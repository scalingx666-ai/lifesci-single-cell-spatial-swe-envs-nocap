# Issue

**Title:** Fix plotGene scale.by functionality

## Description

Allow non-highly variable genes to be scaled by dataset. Add user
option for log2 transform.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c57dd529c920`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.