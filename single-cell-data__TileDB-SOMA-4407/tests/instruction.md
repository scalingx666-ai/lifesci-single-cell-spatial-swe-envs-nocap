# Issue

**Title:** [python] Update Cloud tests to use SOMAContext

## Description

Update the TileDB-SOMA legacy cloud remote tests to use `SOMAContext` instead of the deprecated `TileDBSOMAContext`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28967a5484e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.