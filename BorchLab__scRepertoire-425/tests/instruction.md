# Issue

**Title:** Improve performance of `.lvCompare()`

## Description

A general improvement on the runtime of `combineBCR()` by accelerating `.lvCompare()` with rcpp by a small constant factor.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9a4a123dce1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.