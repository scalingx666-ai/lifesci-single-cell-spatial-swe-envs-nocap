# Issue

**Title:** [python] Deprecate using `None` when creating new SOMA array types

## Description

**Issue and/or context:** Towards SOMA-408

**Changes:**
* Clean-up docstrings
* Add a deprecation warning for adding `None` in the SOMASparseNDArray shape
* Add a deprecation warning when leaving `domain=None` when creating a dataframe type

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ce8c4ce6000`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.