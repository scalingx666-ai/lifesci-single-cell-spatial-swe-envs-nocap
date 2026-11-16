# Issue

**Title:** [ci] Fix issue where we are unable to checkout tag

## Description

**Issue and/or context:** Closes SOMA-580

**Changes:**
Small changes to the CI to fix failed python tests on release.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e2c8682a713`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.