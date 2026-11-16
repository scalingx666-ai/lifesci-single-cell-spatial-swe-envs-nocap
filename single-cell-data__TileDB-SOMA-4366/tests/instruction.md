# Issue

**Title:** [ci] Temporarily disable remote storage workflow

## Description

**Issue and/or context:** Towards SOMA-800

**Changes:**
Disable remote storage workflow on PR/push until the tokens are updated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1f6a685b475`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.