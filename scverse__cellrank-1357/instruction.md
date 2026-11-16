# Issue

**Title:** Add Signal API to plot obs/obsm quantities along trajectories

## Description

## Summary

. Adds a `Signal` abstraction so trajectory plots can fit **any observation-aligned quantity that varies continuously along pseudotime** — not just gene expression. This covers the original request (plot a precomputed gene module score) and generalizes it to `.X`/layers/`.raw`, `.obs` covariates, and `.obsm` columns.

The motivation: "which obs-aligned signal to fit" was previously smeared across three loosely-coupled parameters (`gene` + `data_key` + `use_raw`), which is why `.obsm` couldn't be expressed and `data_key` was ambiguous. A `Signal` makes it **one self-describing value**.

## New public API (`cellrank.models`)

```python
from cellrank.models import Gene, Obs, Obsm

cr.pl.gene_trends(adata, model, "Gata1")                     # str -> Gene from .X (shorthand)
cr.pl.gene_trends(adata, model, Gene("Gata1", layer="Ms"))   # a layer
cr.pl.gene_trends(adata, model, Gene("Gata1", use_raw=True)) # raw
cr.pl.gene_trends(adata, model, Obs("module_score"))         # an .obs covariate / module score
cr.pl.gene_trends(adata, model, Obsm("X_pca", 0))            # .obsm array column
cr.pl.gene_trends(adata, model, Obsm("palantir", "pt"))      # .obsm DataFrame column
cr.pl.gene_trends(adata, model, ["Gata1", Obs("module_score")])  # mix freely
```

Each `Signal` is a frozen dataclass owning its own `fetch`/`validate`/`name`/`ylabel`; adding a new source is a new subclass with no signature churn.

## Changes

- **`Signal`/`Gene`/`Obs`/`Obsm`** — new module `src/cellrank/models/_data.py`, exported from `cellrank.models`, documented in `docs/api/models.md`.
- **`BaseModel.prepare(signal, ...)`** — fetch branching collapses to `signal.fetch(adata)`; new `.signal` property.
- **`gene_trends`** — `genes` → `signals` (accepts `Signal`s or bare names); per-figure neutral y-label (`"value"`) for non-gene signals; per-signal validation.
- **Fan-out** (`_create_callbacks`/`_fit_bulk`) threads a `signals` map to `prepare`; **`heatmap`/`cluster_trends`** route through the same machinery (no public change, no internal warnings).

## Backward compatibility

The legacy `gene`/`data_key`/`use_raw` (on `prepare`) and `genes`/`data_key`/`use_raw` (on `gene_trends`) still work, folded into the equivalent `Signal`. Bare gene-name strings are unchanged and warning-free.

Versioning per the 2.3 → 2.4 plan:
- New API marked `.. versionadded:: 2.3`.
- Legacy params emit a `DeprecationWarning` reading **"will be deprecated in CellRank 2.4"**; `.. deprecated:: 2.4` directives are in place for the formal 2.4 deprecation.

## Tests

- `TestSignals` + `TestPrepareSignal` (21 tests): fetch/validate/name/ylabel for all three sources, `prepare` with each, deprecation warnings, error contracts.
- New `gene_trends` tests for Obs/Obsm/mixed/neutral-ylabel + deprecation-path coverage; existing smoke tests migrated onto the `Gene` API.
- **463 passed, 21 skipped** across `test_plotting`/`test_model`/`test_utils`; `pre-commit` (ruff check + format) clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `561ebbb505df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.