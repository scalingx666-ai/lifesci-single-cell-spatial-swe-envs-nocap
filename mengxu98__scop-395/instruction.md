# Issue

**Title:** fix(spatial): accept object alias for native spatial APIs

## Description

## Summary
- accept `object =` as a backwards-compatible alias for the Seurat input in native spatial QC, plotting, network, and spatial-variable-feature APIs
- reject ambiguous calls that provide both `srt` and `object`, with a clear input error when neither is supplied
- update spatial examples and generated Rd usage to demonstrate the consistent named-object form
- add an end-to-end regression test covering QC, spot/network/SVF plots, KNN storage, and input validation

## Validation
- `pkgload::load_all('.', quiet = TRUE, compile = FALSE)`
- `testthat::test_file('tests/testthat/test-spatial-object-alias.R')`
- targeted spatial tests: `test-spatial-core.R`, `test-spatial-utils.R`, `test-spatial-network-receipt.R`, `test-spatial-variable-features.R`, `test-spatial-run-receipt.R`
- independent `R CMD INSTALL --preclean` succeeded on Windows R 4.5.2

The required `rcmdcheck` wrapper reached package checks but exited while parsing the very large Windows compiler output (`embedded nul`); this is recorded as an environment/tooling limitation, not as a passing full check.

Existing unstaged thin-receipt work was intentionally kept out of this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `359c1a9fbdac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.