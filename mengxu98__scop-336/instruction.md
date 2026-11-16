# Issue

**Title:** feat: add optional Cell2fate wrapper

## Description

Split from #335 so the validated Cell2fate integration can be reviewed independently of CHOIR.

## Summary

- add `RunCell2fate()` for raw spliced/unspliced Seurat assays
- prepare a standalone Python 3.9 `cell2fate_env` with the upstream backend pinned to commit `c03d1ca0bb963f550001c6070d4986a61ec8456a`
- persist model, posterior H5AD, logs, ownership metadata, and a reproducible manifest under `result_dir`
- support safe resume/overwrite behavior and optional dense velocity loading
- write posterior time, uncertainty, module states, and selected-cell status to Seurat metadata, with provenance in `srt@tools`
- keep Cell2fate runtime-optional and leave `DESCRIPTION` unchanged

## Verification

- `testthat::test_file("tests/testthat/test-cell2fate.R")`: 43 passed, 0 failed, 0 warnings, 0 skipped
- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)`: passed
- local R CMD check without remote CRAN incoming: 0 errors, 0 warnings, 1 pre-existing Rd cross-reference note
- real `pancreas_sub` smoke: 80 cells, 50 genes, 2 modules, 7 Cell2fate metadata columns, manifest complete, pinned backend commit observed
- Python runner syntax check and backend provenance check passed

The exact `--as-cran` command was also attempted, but the local run stalled at the remote CRAN incoming feasibility step before package code checks began.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e99d30ff51cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.