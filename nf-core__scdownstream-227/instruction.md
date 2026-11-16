# Issue

**Title:** Make mito percentage calculation more flexible

## Description

- Bug fix: Mito percentage filtering now uses the `symbol_col` specified in the samplesheet to check for the `mt-` prefix
- Feature: New optional parameter `mito_genes`, as an alternative to checking for the `mt-` prefix. Expects a file with one gene per row.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `facf1a8bbe89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.