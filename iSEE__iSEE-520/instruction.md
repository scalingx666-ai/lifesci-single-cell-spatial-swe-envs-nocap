# Issue

**Title:** Force uniqueness of all names via cleanDataset.

## Description

A more generic solution of #518, which allows SE subclasses to define additional cleaning methods for their slots.

Note that this relies on a fix to the SCE name setting behavior, to be pushed in a bit.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `98281a1b8d12`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.