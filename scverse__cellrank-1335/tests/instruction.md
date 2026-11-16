# Issue

**Title:** fix(pl): reuse fitted models passed back to gene_trends

## Description

## Problem

.

Models returned by `cr.pl.gene_trends(..., return_models=True)` could not be reused. Passing the returned `{gene: {lineage: model}}` dict back as the `model` argument recomputed every trend instead of reusing the fitted values.

**Root cause:** `_create_models` copies each supplied model with `copy.copy`, and a model's `__copy__` deliberately resets the `prepared` flag (models are treated as templates to fit afresh). So `_fit_bulk_helper` re-prepared and re-fit each model from scratch. The only object that survives copying with its fitted data intact is `FittedModel`, but nothing converted the returned `GAM`/`SKLearnModel` objects to that type.

## Fix

Added `_copy_or_reuse_model` in `src/cellrank/pl/_utils.py`: if a model is already prepared and has predicted values (`y_test`), it is wrapped in a `FittedModel` (whose `prepare`/`fit`/`predict` are no-ops returning the stored values); otherwise it is copied as a fresh template, exactly as before.

This is applied **only** to the gene- *and* lineage-specific assignment in `_create_models` — the canonical shape of the returned dict. The `*` fallback and single-model template paths still use plain `copy.copy`, because fanning a fitted model across multiple lineages would wrongly apply one lineage's trend to the others (and a single `FittedModel` already round-trips correctly through `copy.copy`).

The user's expected usage now works:

```python
models = cr.pl.gene_trends(adata, model=model, genes=..., return_models=True, ...)
cr.pl.gene_trends(adata, model=models, genes=..., ...)  # reuses, no refit
```

## Other changes

- Documented the reuse capability in the shared `return_models` docstring (`_docs.py`), which flows into `gene_trends`, `heatmap`, etc.
- Added `test_reuse_returned_models` to `TestGeneTrend` verifying the second call returns `FittedModel` instances with identical `x_test`/`y_test`.

## Verification

- New test plus existing `TestGeneTrend`, `TestHeatmap`, `TestHeatmapReturns`, `TestClusterTrends`, `TestFittedModel` (plotting + model), and `TestCreateModels` all pass.
- pre-commit (ruff check/format) clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `187e167ab340`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.