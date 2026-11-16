# Issue

**Title:** Improving downstream analysis NMF workflow

## Description

- [x] More options to control the dotplot and spatial visualisation
- [ ] Subset cell types 
- [x] Subset locations - solved by using `adata.obsm` rather than `uns['mod']` as input.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a65d67b216d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.