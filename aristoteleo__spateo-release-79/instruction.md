# Issue

**Title:** Negative binomial mixture variational inference

## Description

Implemented a variational inference model for negative binomial mixture because it scales better with many samples.

EM-based mixture model scales approximately linearly in the number of samples, whereas the VI model scales logarithmically, so it can be run with less downsampling (and more complete data).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55c7281e90ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.