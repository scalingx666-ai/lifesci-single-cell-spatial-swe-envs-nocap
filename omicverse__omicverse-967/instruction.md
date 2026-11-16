# Issue

**Title:** docs(pp): clarify QC filtering order

## Description

Clarify that doublet detection runs after QC threshold filtering and
final cell/gene filtering. Correct outdated AnnData input/return
descriptions and document min_cells and batch_key using the existing
docstring format.

Documentation only; no runtime behavior changes.

Validation: git diff --check passed; executable AST unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5994359e2c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.