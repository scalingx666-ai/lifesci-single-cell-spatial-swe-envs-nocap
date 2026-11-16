# Issue

**Title:** Update graph_fitting.py

## Description

EPG elastic curve was actually never added to adata.uns. It lead to errors during pseudotime calculation. Should work now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `408e7b5410ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.