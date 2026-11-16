# Issue

**Title:** Issue52

## Description

1. force index in df_cov and df_score to be str. adata.obs_names is automatically string when the cell names are `1`, `2`, ....  (commit 19da98301842333909c3e8a4c68b67e349784a74)
2. add --min-genes and --min-cells in CLI for customized filtering; add the corresponding info in the website doc (commit a0ea123c5a499c3c52f36622d6621b2ae576b526)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c227120759c5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.