# Issue

**Title:** feat(pp): support custom keys in ov.pp.regress

## Description

Add optional ``keys`` parameter to ``ov.pp.regress``, defaulting to ``['mito_perc', 'nUMIs']`` for full backward compatibility. Users can now regress out arbitrary ``adata.obs`` columns, such as cell-cycle scores (``S_score``, ``G2M_score`` from ``ov.pp.score_genes_cell_cycle``) or
ribosomal gene percentage.
A validation guard raises ``KeyError`` with the list of available columns when a requested key is missing from ``adata.obs``. Updated ``register_function`` metadata and docstring accordingly.
Related to #798 .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5307e30e377c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.