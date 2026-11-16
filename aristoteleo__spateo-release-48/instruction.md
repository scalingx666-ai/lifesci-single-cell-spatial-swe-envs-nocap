# Issue

**Title:** update plotting

## Description

1. convert geometric object to `Well Known Binary`  (WKB) representation using shapely, so the adata can be saved as a h5ad file.
2. update `geo`, `space` and `colorlabel` functions

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b6375c843c52`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.