# Issue

**Title:** fix: preserve LIANA consensus export semantics

## Description

﻿## Summary

- preserve the field set returned by LIANA's official consensus mode
- fill deterministic ligand-receptor interaction identifiers during SCOP standardization/export
- avoid adding all-`NA` aggregate/significance placeholders to rank consensus results
- avoid adding all-`NA` magnitude/specificity placeholders to aggregate consensus results

## Root cause

LIANA 0.1.14 `rank_aggregate()` returned complete rows, but SCOP's unified standardization added fields from the other consensus mode and significance fields that are not defined for LIANA ranks. Existing-but-empty interaction columns also prevented `ccc_to_liana()` from using its deterministic ligand-receptor fallback.

## Semantics

This does not impute LIANA statistics or convert rank-like support into a significance call. Rank consensus keeps the official magnitude/specificity fields; aggregate consensus keeps the official aggregate rank. SCOP-only display identifiers are derived from ligand and receptor names.

## Validation

- `pkgload::load_all('.', quiet=TRUE, compile=FALSE)`
- `testthat::test_file('tests/testthat/test-ccc-platform-v2.R')`
- real LIANA 0.1.14 sham result: 7,184 rows; official consensus 0 NA; standardized consensus 0 NA; `ccc_to_liana()` export 0 NA; interaction keys and magnitude/specificity ranks unchanged
- `_R_CHECK_FORCE_SUGGESTS_=false rcmdcheck --as-cran --no-examples --no-tests --no-manual`: 0 errors; existing upstream warnings remain for optional `CellChat`/`nichenetr` namespace checks and undeclared infercnv/numbat test imports; unstated dependencies in examples is OK

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3ede6bcb1e6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.