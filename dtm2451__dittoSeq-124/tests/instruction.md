# Issue

**Title:** small bug fix in dimensionality reduction grabbers

## Description

Full fix for #122

The fix: Catch outputs that are equivalent to 'no reductions in the object' for both Seurat and SCE objects in `getReductions()` and ensure these output as 'NULL'.  Doing so allows the error catch already in `.default_reduction()` to be properly triggered.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2edebdd98ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.