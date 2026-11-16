# Issue

**Title:** pp.scdblfinder: default doublet rate 1% per 1000 cells, as R scDblFinder

## Description

`ov.pp.scdblfinder` (and `ov.pp.qc` with the default `doublets_method='scdblfinder'`) inferred the expected doublet rate as 0.8% per 1000 cells. R scDblFinder and pyscdblfinder ≥ 0.3.1 use 1% per 1000 cells; this changes the default to 0.01 so omicverse calls match R. Docstring: `n_features` are the most-expressed genes (R `rowMeans` order), not the most variable.

Related: pyscdblfinder 0.3.1/0.3.2 (omicverse/py-scDblFinder#7, #9) port the RNA path step by step from R scDblFinder 1.16.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b72c16630fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.