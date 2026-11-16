# Issue

**Title:** [ci] Remove github workflow tiledb-py pin

## Description

**Issue and/or context:** Closes SOMA-373

**Changes:**
Remove pin that was temporarily needed while release process was underway for release 2.28.1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `389511daa07e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.