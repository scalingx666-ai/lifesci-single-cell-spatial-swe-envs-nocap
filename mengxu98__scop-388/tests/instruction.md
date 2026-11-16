# Issue

**Title:** chore: clean stale spatial backend surfaces

## Description

## Summary
- remove the obsolete SpatialQM optional-backend matrix entry
- align README, NEWS, the Giotto bridge article, and SpatialGradient docs with the backends that remain in 0.9.1
- stop recording a nonexistent SPATA2 version for the native C++ gradient path
- bound the live Giotto round-trip without converting timeouts into passing skips

## Validation
- `test-spatial-gradient.R`: passed with compiled native code
- `test-framework-bridges.R`: passed, including the real GiottoClass round-trip
- `pkgload::load_all('.', quiet = TRUE, compile = FALSE)`: passed
- `tools::checkRd()` plus `tools::Rd2ex()`/`parse()` for `RunSpatialGradientFeatures.Rd`: passed
- `rmarkdown::render()` for `spatial-framework-bridges.Rmd`: passed
- optional-backends YAML parsed and no longer contains `spatialqm`
- `git diff --check`: passed
- prescribed local `rcmdcheck`: 0 errors, 2 inherited warnings, 4 inherited notes; unstated example dependencies check passed. The warnings concern existing lifecycle/glmGamPoi/sctransform declarations and unrelated Rd usage entries, not files changed here.

## Scope
This PR does not restore the removed spatial registry, add a new backend, or change the current C++ gradient algorithm.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `06a934438d9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.