# Issue

**Title:** Support `.obsm` proportion frames for macrostate naming

## Description

## Overview

Towards CellRank analysis on **samples** (not just individual cells). Sample embeddings come from SE (`sinkhorn_embeddings`), where each sample is summarized by a distribution over some categorical covariate (cell type, condition, disease status, …) stored as a per-observation proportion frame in `adata.obsm`.

This extends `GPCCA.compute_macrostates(cluster_key=...)` to name macrostates from such an `.obsm` proportion frame, in **addition to** the existing `.obs` categorical path. It mirrors the obs/obsm duality that #1321 added to `plot_macrostate_composition` and reuses its machinery.

## What changed

`cluster_key` is now `str | Mapping[str, str]`:

```python
# obs categorical (unchanged):
g.compute_macrostates(n_states=7, n_cells=20, cluster_key="cell_type")

# .obsm proportions — each macrostate named by its dominant covariate category:
g.compute_macrostates(n_states=7, n_cells=20, cluster_key={"obsm": "cell_type"})

# weighted by per-sample cell counts (obsm-only):
g.compute_macrostates(n_states=7, n_cells=20, cluster_key={"obsm": "cell_type"}, weight_key="n_cells")
```

- `{"obsm": <key>}` points to a `DataFrame` whose columns are categories and whose rows are per-observation proportions summing to 1. Each macrostate is named after the category with the largest **(weighted) summed proportion** among its most-likely observations.
- New obsm-only `weight_key` scales each row by a per-sample weight (e.g. cell count), so naming can reflect cell-level rather than sample-level dominance. Default is equal weighting.
- With equal weights and one-hot proportions, naming and colors reproduce the `.obs` path **byte-identically** (this is the gate test).

## Implementation (reuse-first)

- **`_utils/_colors.py`** — extracted the shared `association table → names + colors` tail of `_map_names_and_colors` into `_names_and_colors_from_association`; added a soft-assignment front-end `_map_names_and_colors_from_proportions` that builds the association table by summing weighted proportion rows, then delegates to the shared tail (so argmax-naming, `_1/_2` dedup, and color shifting are identical to the obs path).
- **`_utils/_utils.py`** — promoted `_resolve_composition_key` out of `GPCCA` (the base estimator can't reach a GPCCA staticmethod) and added `_obsm_proportions` (positional realignment to `obs_names`), `_check_proportions` (rows sum to 1, `atol=1e-3`), and `_obsm_proportion_weights`. `plot_macrostate_composition`/`_obsm_composition` now reuse these, single-sourcing the proportion-validation/weight rules.
- **Shared base** — the obs/obsm branch lives in `_set_categorical_labels`, so `set_terminal_states`/`set_initial_states` (incl. CFLARE) gain `{"obsm": ...}` for free.
- **TSI stays obs-only** — `tsi` round-trips `cluster_key` through `.uns` for cache validity, so it raises a clear `TypeError` if a `Mapping` is passed.

## Tests

- `test_colors.py`: one-hot ↔ hard-count equivalence, dominant-category, weighting changes the name, duplicate-dominant dedup, NaN-query handling, error paths.
- `test_gpcca.py`: obs vs obsm naming **and color** equivalence, `{"obs":...}` == bare string, weighted run, `n_states=1`, `_obsm_proportions` positional alignment, and the full error matrix (missing key, non-DataFrame, rows not summing to 1, `weight_key` with obs source, missing weight column, invalid dict source, TSI rejecting a Mapping).
- No regression in the #1321 `TestMacrostateComposition` image tests.

## Reviewer notes

- Scope was deliberately kept to **naming only**. Follow-up candidates for sample-level support (out of scope here): `pl.aggregate_fate_probabilities`, `compute_lineage_drivers`, soft coloring in `pl.heatmap`/`log_odds`/`gene_trends`, kernel `cbc`, and obsm-based TSI.
- One subtlety handled: `pd.get_dummies` of a categorical yields a `CategoricalIndex` for columns, which rejects the bookkeeping columns the dedup tail appends — normalized in `_names_and_colors_from_association`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `099c43bc60b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.