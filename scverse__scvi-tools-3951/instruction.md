# Issue

**Title:** Backport PR #3950 on branch 1.5.x (fix: defer huggingface_hub import in scvi.hub to point of use)

## Description

Backport PR #3950: fix: defer huggingface_hub import in scvi.hub to point of use

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49481a167f1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.