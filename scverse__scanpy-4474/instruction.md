# Issue

**Title:** Backport PR #4401 on branch 1.12.x (fix: have ingest no longer truncate to settings.N_PCS)

## Description

Backport PR #4401: fix: have ingest no longer truncate to settings.N_PCS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dce8af65d24c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.