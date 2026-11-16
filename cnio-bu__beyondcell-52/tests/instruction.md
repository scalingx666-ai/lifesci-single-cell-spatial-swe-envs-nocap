# Issue

**Title:** Give a value to n.genes slot of GenerateGenesets' output

## Description

The current value is `NaN`, though the actual value should be a real number in order to compute the background matrix if necessary. With this commit, the value is now computed as the median number of genes per signature in the input gmt.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c5a547e9bc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.