# Issue

**Title:** Fix and refactor `filter_genes`

## Description

## Bug fixes

* `filter_genes` now works with `adata.layers['unspliced']` being sparse and `adata.layers['spliced']` dense.

## New

* Adds function `multiply` for element-wise multiplication of arrays and sparse matrices

## Changes

* Refactors `filter_genes` to make use of `multiply` and fix #533.

## Related issues

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba75c4a14b50`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.