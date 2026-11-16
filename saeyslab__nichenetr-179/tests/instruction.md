# Issue

**Title:** Preserve plot labels when only one ligand/target pair is detected

## Description

When a single ligand/target pair is detected, subsetting the `active_ligand_target_links` matrix leads to a loss of row and column names. Adding `drop = FALSE` fixes the issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90bce8bcaadf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.