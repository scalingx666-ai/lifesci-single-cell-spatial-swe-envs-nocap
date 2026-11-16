# Issue

**Title:** Abandon snapshot-based tests for hugo-unifier

## Description

This is necessary because recently the HUGO API changed their exact return values frequently multiple times, leading to hash changes in the processed anndata files

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59069401a69b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.