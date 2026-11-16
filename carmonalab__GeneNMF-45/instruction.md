# Issue

**Title:** Add renameMetaPrograms function for renaming MPs in GeneNMF results

## Description

This PR introduces a new utility function `renameMetaPrograms` for renaming meta-programs in GeneNMF analysis results. This function allow users to assign new names to existing meta-programs, and ensures all associated data structures are updated accordingly. Comprehensive documentation has also been added.

This is especially useful under 2 conditions:
- to rename and reorder MPs based on similar biological functions (eg. MP1/3/5 cell cycle, MP2/4/6 EMT -> MP1-3 cell cycle, MP4-6 EMT).
- to revise discontinuous MP names after filtering by `dropMetaPrograms` (eg. MP1/3/4/5 after filtering out MP2 -> MP1/2/3/4)

Core scripts are adapted from `getMetaPrograms` and tested on my local machine.
https://github.com/carmonalab/GeneNMF/blob/355c4664732ab9a5a62f1b7c38faca8bf3c4c689/R/main.R#L268-L302

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `355c4664732a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.