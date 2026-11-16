# Issue

**Title:** [ci] Remove the ubuntu-src dockerfile

## Description

**Issue and/or context:** Closes SOMA-689

**Changes:**
Remove ubuntu-src dockerfile. This dockerfile is redundant as it install the python API indirectly through pip anyway.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cadd80f817a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.