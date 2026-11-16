# Issue

**Title:** Fix cell order bug in subsetLiger

## Description

This bug previously caused discrepancies in cell order between cell.data and other slots.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d32067aa286`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.