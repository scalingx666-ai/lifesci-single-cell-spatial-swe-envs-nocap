# Issue

**Title:** fix: allow Milo neighborhood proportion plots

## Description

## Problem
`RunMilo()` stores both group-level and neighborhood-level results, and the internal plotting helper already supports both. However, the exported `ProportionTestPlot()` wrapper declares `result_level = c("group")`, so `result_level = "neighborhood"` fails in `match.arg()` before the stored Milo results are read.

## Change
- allow `result_level = "neighborhood"` in `ProportionTestPlot()`
- update the generated documentation
- add a regression test for the public argument contract

## Validation
- `testthat::test_file("tests/testthat/test-proportion-log2fd.R")`
- Result: 12 tests passed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b022f2c1918`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.