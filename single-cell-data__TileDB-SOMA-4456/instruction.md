# Issue

**Title:** [c++] Perf: Make arrow conversion async

## Description

**Issue and/or context:** TileDB to Arrow column conversion was single threaded but should be async

**Changes:**

**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a59c3ef42df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.