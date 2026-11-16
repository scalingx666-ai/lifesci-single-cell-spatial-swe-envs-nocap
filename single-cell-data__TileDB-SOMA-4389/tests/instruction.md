# Issue

**Title:** [c++] Temporarily roll back vcpkg changes

## Description

**Issue and/or context:** Fixes SOMA-784

**Changes:**

The vcpkg changes broke the packaging CI. Rollback the changes until we have time to update the python packaging as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4ab22ff44a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.