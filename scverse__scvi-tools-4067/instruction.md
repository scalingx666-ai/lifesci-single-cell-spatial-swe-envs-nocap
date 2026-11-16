# Issue

**Title:** Backport PR #4066 on branch 1.5.x (fix(scanvi): register from_scvi_model datamodule registry as SCANVI so the model can be reloaded)

## Description

Backport PR #4066: fix(scanvi): register from_scvi_model datamodule registry as SCANVI so the model can be reloaded

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d10f657c2b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.