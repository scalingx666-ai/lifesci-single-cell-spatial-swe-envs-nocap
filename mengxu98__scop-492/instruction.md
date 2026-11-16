# Issue

**Title:** wip(scenicplus): native SCENIC+ backend in C++ with tests

## Description

## Summary
- Add native SCENIC+ entry points in `src/SCENIC.cpp`, and update `R/RunSCENICPlus.R` plus its docs.
- Add `tests/testthat/test-scenicplus-native.R` and adjust the GRNBoost sparse test. `RcppExports` comes from a clean `Rcpp::compileAttributes()` run.

## Test plan
- [ ] Run `tests/testthat/test-scenicplus-native.R`
- [ ] Run `tests/testthat/test-scenic-grnboost-sparse.R`
- [ ] Confirm `RunSCENICPlus` help matches the new native backend arguments

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `083f5f31e372`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.