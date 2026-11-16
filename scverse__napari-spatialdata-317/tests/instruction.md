# Issue

**Title:** Fix bug adata in model not being reset

## Description

Fixes two bugs:
- there was a hardcoded `genes_color`, I fixed this
- if an element with a table was added and removed, the `mode.table` was not being reset, leading to inconsistent behavior

CC @melonora

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4385a20a1439`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.