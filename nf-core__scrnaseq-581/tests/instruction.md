# Issue

**Title:** Increase runtime limits for cellranger and cellbender processes

## Description

The 240h runtime matches the earlier pipeline allowance for long-running processes introduced in PR .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a34bdc6b38ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.