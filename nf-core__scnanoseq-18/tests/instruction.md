# Issue

**Title:** Various updates: Fix #17, disables umi-tools qc in MultiQC, adds missing versions and updates outputs

## Description

Main changes here include the following:

- Fix #17 
- Places hold on #12 to not overcrowd the MultiQC report
- Adds missing Seurat version in main workflow
- updates output.md (ToulligQC figures are now from `test_full`, along with other minor changes) + adds ToulligQC citation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `683b53cc42d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.