# Issue

**Title:** FindConservedMarkers update to filter out nan p values

## Description

Following  , I have added a line in [seurat/R/differential_expression.R](https://github.com/satijalab/seurat/blob/9755c164d99828dbc5dd9c8364389766cd4ff7fd/R/differential_expression.R#L407) to filter out nan values if any.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38e825a64b13`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.