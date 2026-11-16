# Issue

**Title:** use just one batch of pancreas data

## Description

Removes batch as a covariate, which might be causing bad performance.

Benchmark passing at https://github.com/scottgigante-immunai/openproblems/actions/runs/3322839154

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2512dd3073a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.