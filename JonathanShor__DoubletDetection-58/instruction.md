# Issue

**Title:** V1.2 Hypergeometric p-Values

## Description

• Better performance calling doublets by computing a p-value from hypergeometric testing on the level of synthetic doublet enrichment in each cluster.
• Multiple runs can be specified to produce significantly better p-values. Our recommendation, and the default setting, is 5 runs.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85a8e736404f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.