# Issue

**Title:** [r] Fix check to enable GRanges conversion

## Description

This should fix #229, which is likely caused by a combination of specific installation procedures and the BPCells R package getting built before the GenomicRanges package is installed.

For what it's worth, I don't reproduce issue #229 on a fresh `renv` environment when running `renv::install("bnprks/BPCells/r@v0.3.0")`, followed later by `renv::install("bioc::GenomicRanges")`.

Since we want these conversion functions to work regardless of how/when BPCells was installed, wrapping this in an `rlang::on_load()` call makes it a load-time rather than an install-time check.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d848ca44ca0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.