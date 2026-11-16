# Issue

**Title:** Cleanup .travis.yml for a custom RcppArmadillo version.

## Description

This cleans up the issues you were hitting in craigcitro/r-travis#162.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `feb0ffce95bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.