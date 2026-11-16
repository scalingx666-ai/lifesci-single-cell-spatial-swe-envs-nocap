# Issue

**Title:** [r] fix issue for `qc_scATAC()` near chromosome starts

## Description

This pull request addresses a bug in the `qc_scATAC()` function that occurred when processing fragments or genes near the start of a chromosome. The changes ensure that genomic region calculations do not produce negative start positions, which could previously cause errors. Additionally, a regression test was added to verify correct handling of these edge cases.
 
**Bug fix for genomic region calculation:**

* Updated the calculation of `start` positions for TSS windows, TSS flanks, and promoters in `qc_scATAC()` to use `pmax(..., 0L)`, ensuring that start positions are never negative. This prevents errors when fragments or genes are close to the chromosome start. (`r/R/atac_utils.R`)

**Testing improvements:**

* Added a regression test to confirm that `qc_scATAC()` correctly handles genes near the start of a chromosome. The test verifies that all expected cell names are present in the output. (`r/tests/testthat/test-atac_utils.R`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f33b8589c02`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.