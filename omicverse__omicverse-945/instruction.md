# Issue

**Title:** fix(single): harden velocity downstream alignment

## Description

## Summary

Audit and harden the existing RNA-velocity downstream paths without changing the `Velo` framework or backend-selection architecture.

- make public `Velo.graphvelo()` work with its documented default `gene_subset=None`
- preserve the selected GraphVelo gene mask instead of marking every gene as a velocity gene
- validate empty or unknown GraphVelo gene subsets before training
- align perturbation velocity matrices by `obs_names` and `var_names` before computing direction-change scores
- reject mismatched or non-unique labels instead of silently comparing unrelated cells or genes

## Root cause

`graphvelo()` indexed `adata.var.loc[gene_subset]` after training. The default `None` therefore failed, while the chained assignment used for explicit subsets subsequently overwrote the entire marker column with `True`.

`velocity_effect()` only checked matrix shapes and compared rows and columns positionally. Two AnnData objects containing the same cells and genes in different orders produced scientifically incorrect scores without an error.

## Impact

GraphVelo downstream output now completes with the default and records an accurate `velocity_gv_genes` mask. RegVelo perturbation comparisons are order-safe for both dense and sparse layers and fail clearly when the objects cannot be aligned.

## Validation

- focused velocity/trajectory suite: 48 passed
- vendored GraphVelo real-data smoke: passed (12 cells, learned transition basis, full-layer and UMAP projections)
- `python -m compileall -q omicverse/single/_velo.py`
- `git diff --check`

The RegVelo and CellRank optional-backend contracts remain mock-tested in the focused suite; this PR does not claim a real RegVelo training run.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c30f9a6ef7a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.