# Issue

**Title:** Fix bug in bcScore

## Description

While checking if Seurat's `@data` and `@counts` matrices are identical

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c280bd8abd9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.