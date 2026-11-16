# Issue

**Title:** `group_split`

## Description

Same as for `tidySiongleCellExperiment`. Just had to import `group_split` from dply and adjust for a difference in `pbmc_small` for tests.

Issue #65

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bad24e7a11f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.