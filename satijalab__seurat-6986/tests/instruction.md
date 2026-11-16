# Issue

**Title:** fix(Xenium): load renamed feature

## Description

The feature type got changed from `Blank Codeword` to `Unassigned Codeword`, so this just loads from the new feature if the the old feature isn't found.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9f6cc3facf01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.