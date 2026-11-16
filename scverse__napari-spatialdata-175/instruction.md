# Issue

**Title:** Plotting annotations fix

## Description

This PR fixes the issue reported in #164. The problem was that when filtering the anndata object it would result in an anndata object with potentially 0 rows. This PR checks whether the anndata object to be added to the metadata has 0 rows. If this is the case then the `adata` metadata is set to be `None`. Also if there is no table, adata will be none, but in addition `region_key` will also be `None`.

In addition to the implementation of @aeisenbarth this handles the case when a table is present, but there are no annotations for a given element.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b906ee24cb45`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.