# Issue

**Title:** Make MulticoreTSNE optional

## Description

Fixed bug where some users, especially windows, have trouble installing MulticoreTSNE. 

Thus, we remove it as a dependency and instead make it optional.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b528327f6239`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.