# Issue

**Title:** More systematic handling of date, title and IDs for browser saves.

## Description

This guarantees a unique ID, regardless of whatever title the user puts in.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65cbdc5c60bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.