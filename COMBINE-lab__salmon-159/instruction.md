# Issue

**Title:** Factorization develop

## Description

The changes (other than adding the range factorization) are:

1- Number of minimum EM operation are set to 100. (works better for small samples of factorization paper)
2- The {:f} option for writing out "count" values are removed. This makes the Spearman correlation of RSEM simulated data 0.8245 in RF mode. (compared to 0.8232 when using the {:f} option)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `81fd2b8d48d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.