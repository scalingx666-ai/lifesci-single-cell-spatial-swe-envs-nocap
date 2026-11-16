# Issue

**Title:** gene expression perf work

## Description

Several small changes to chip away at the gene expression performance regressions:
* missing memoization for expression binning
* don't unnecessarily create transformed state and attach to components
* remove dead code

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0667ad027407`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.