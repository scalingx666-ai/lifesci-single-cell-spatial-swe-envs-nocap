# Issue

**Title:** [r] Remove unused private tiledb_array member

## Description

**Issue and/or context:** Closes SOMA-777

**Changes:**
* Remove unused private method `tiledb_array`
* Remove test functions for deprecated classes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae72049eb0d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.