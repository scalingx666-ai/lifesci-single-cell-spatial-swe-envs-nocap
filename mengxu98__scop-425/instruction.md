# Issue

**Title:** feat(nichenet): export merged ligand target table

## Description

## Summary

- add an optional merged_table_file argument to RunNichenetr()
- export a UTF-8 CSV that expands existing LR rows with ligand activity fields and ligand-target rows
- preserve all existing NicheNet result tables and CCC aggregation behavior
- reject existing output files and missing parent directories before backend execution
- document the ligand-level interpretation of repeated target rows

## Validation

- targeted test-ccc-backend-parity.R: 116 passed, 1 existing skip
- pkgload::load_all(".", quiet=TRUE, compile=FALSE): passed
- R CMD check --no-install --no-manual --as-cran --no-examples --no-tests: 0 errors, 0 warnings, 1 existing note
- full CCC test run: new tests passed; unrelated existing failures remain from the local presto lazy-load database, namespace preload state, and an Ensembl network timeout
- full rcmdcheck reached package installation but was blocked by the current worktree C++ build/embedded-NUL log issue

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1d2a37a89b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.