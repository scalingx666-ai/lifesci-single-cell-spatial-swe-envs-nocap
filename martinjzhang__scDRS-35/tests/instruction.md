# Issue

**Title:** Issue32

## Description

1. Remove genes with ct_mean<0 before calling loess, addressing 
2. Print info for `--adj-prop`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa5b6167db80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.