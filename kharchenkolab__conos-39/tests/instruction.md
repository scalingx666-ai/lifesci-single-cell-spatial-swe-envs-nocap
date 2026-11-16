# Issue

**Title:** Fixed plotting 'groups' and 'gene' together

## Description

Also, removed warning when plotting shorter 'groups' than no. cells, fixed problems with NAs for appendSpecifitiyMetrics, changed warning to stop when 'gene' is not in the data since it only produces NAs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d956d34174bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.