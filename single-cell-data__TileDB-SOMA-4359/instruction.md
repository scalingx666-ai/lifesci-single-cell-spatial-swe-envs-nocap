# Issue

**Title:** [python] Use arrow API to cast python tables before sending to C++

## Description

**Issue and/or context:** Close SOMA-721

**Changes:**
Use pyarrow API to attempt to cast data before writing with the C++ API.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7629a25b3dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.