# Issue

**Title:** Debug the dyn.pl.kinetic_curves()

## Description

Debug several issues related to kinetic_curves:

- [x] `exprs` calculation from umap inverse transform doesn't work.
- [x] `exprs` and `time` are not correctly indexed in `fetch_exprs()`
- [x] `valid_genes` output lost the input order discussed .
- [x] `ddhodge` need a basis parameter.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcfa5e00a6cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.