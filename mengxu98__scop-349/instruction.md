# Issue

**Title:** fix: discover LIANA resources across R libraries

## Description

﻿## Summary

- keep the required optional-backend `check_r()` probe
- use successful resolution of LIANA's official `show_resources()` as the authoritative availability check
- add a regression test for installations where LIANA is resolvable from a non-primary R library

## Root cause

`check_r()` checks its default library path and can report `FALSE` when LIANA and SingleCellExperiment are installed in another entry of `.libPaths()`. `get_namespace_fun()` can still resolve and call the official backend, but `ListCCCDB()` returned early and incorrectly reported LIANA as unavailable. This also rejected `MouseConsensus` before analysis.

## Validation

- `testthat::test_file("tests/testthat/test-ccc-platform-v2.R")`
- real backend smoke test: 19 LIANA resources discovered, including one `MouseConsensus`
- `pkgload::load_all(".", quiet = TRUE, compile = FALSE)`
- local R CMD check without CRAN incoming network probe reached `checking for unstated dependencies in examples ... OK`; existing CellChat/nichenetr dependency warning is unrelated to this diff

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c58a2071cdad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.