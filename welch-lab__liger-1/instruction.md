# Issue

**Title:** Improve quantile_align_SNF and distortion_metric functions

## Description

Use irlba_prcomp to speed up distortion metric calculation.
Add option for separate distortion metric for datasets.
Report summary of unaligned cells in quantile_align_SNF.

Also added option to calculate agreement on aligned factors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edab045fab48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.