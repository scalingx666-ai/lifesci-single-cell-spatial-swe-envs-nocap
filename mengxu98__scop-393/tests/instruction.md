# Issue

**Title:** feat: drop low-cell samples in RunDEtest pseudobulk DE

## Description

## Summary
- Add `min.cells.sample` (default `10`) to sample-level `RunDEtest()` so pseudobulk samples with too few cells in the current `group.by` level are dropped before edgeR/limma/DESeq2/dream.
- This prevents a tiny donor from reversing sample-level logFC relative to cell-level tests; dropped samples are recorded in `sample_inventory`. Use `min.cells.sample = 1` to keep the previous unfiltered behavior.

## Test plan
- [ ] `testthat::test_file("tests/testthat/test-rundetest-min-cells-sample.R")` reproduces the sign flip at `min.cells.sample = 1` and restores direction at the default of 10
- [ ] `testthat::test_file("tests/testthat/test-atac-differential-accessibility.R")` still reaches sample-level methods with `min.cells.sample = 1`
- [ ] On a real multi-donor object, confirm low-cell samples are listed in `srt@tools$DEtest_*$sample_inventory` and groups with fewer than 2 remaining samples per condition are skipped

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `840b087abad1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.