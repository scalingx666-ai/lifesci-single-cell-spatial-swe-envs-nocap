# Issue

**Title:** Release v1.3.0 - First pip-installable version

## Description

# Release v1.3.0

This is the first pip-installable version of BANKSY.

## New in v1.3.0
-  Pip-installable: `pip install banksy_py` (and from git and source)
-  Modern src/ layout (PEP 517/518 compliant)
-  Python 3.8-3.12 support
-  Optional dependencies: `[notebooks]`, `[mclust]`, `[all]`
-  IPython optional

## Carried Forward from v1.2.1
- AGF correction (aligns with R version)
- `num_neighbours` parameter (was `k_geom`)
- CODEX and DLPFC multi-sample examples

Ready for PyPI upload after merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8334998ab674`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.