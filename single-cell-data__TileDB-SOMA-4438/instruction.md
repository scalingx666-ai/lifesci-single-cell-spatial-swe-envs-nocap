# Issue

**Title:** [ci] Update/reduce docker CI

## Description

**Issue and/or context:** Closes SOMA-903

**Changes:**

- Remove chron job
- Only one version of SOMA per docker instance
- Use latest SOMA release

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0b669e8b829`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.