# Issue

**Title:** [r] Deprecate allowing domain to be left as NULL

## Description

**Issue and/or context:** Towards SOMA-408

**Changes:**
* Add lifecycle as a dependency
* Add a deprecation warning for setting `domain` to `NULL` in `SOMADataFrame`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f5c6d5268c47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.