# Issue

**Title:** First set of updates.

## Description

Hello! I have a few basic updates for this pull request, namely:
- Added function to make DGEs from bedmap output
- Added parameter for choosing which datasets to include variable genes from
- Added an extra condition to the check for repeated cell names in createLiger so that inputting a single dataset does not result in an error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea7f5f5fb58c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.