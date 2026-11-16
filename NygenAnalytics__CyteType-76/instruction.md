# Issue

**Title:** Gene symbols patch

## Description

Catch entrez ids 
raise error if auto-detection of gene symbol column contains gene ids > 50%

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6afd9802fc0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.