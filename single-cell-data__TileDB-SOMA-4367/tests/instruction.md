# Issue

**Title:** [python] Add function to cast for old versions of pyarrow

## Description

**Issue and/or context:** Closes SOMA-801

**Changes:**
Add function to do `pyarrow.RecordBatch` cast internally since `cast` method is not included in pyarrow version 11.0.0 (current minimum version).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b4b2b9258eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.