# Issue

**Title:** Replace `louvain` with `leiden`

## Description

Replace `louvain` with `leiden` as the default clustering method for its better performance and maintenance.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5a199886f83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.