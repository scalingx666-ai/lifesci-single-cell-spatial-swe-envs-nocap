# Issue

**Title:** Normalize method results to baseline scores

## Description

.

This PR uses baseline methods to force all scores to range from 0 to 1. Methods that score worse than the worst baseline will have scores <0; methods that score better than the best baseline will score >1. Tasks with <2 baselines will treat all methods as baselines for normalization purposes. 

Baseline methods are then removed, and methods are scored on the average scaled metric instead of the average metric rank.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21eca6df9adf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.