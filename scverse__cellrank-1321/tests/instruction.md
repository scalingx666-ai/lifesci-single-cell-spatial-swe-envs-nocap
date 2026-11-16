# Issue

**Title:** Support `.obsm` proportion frames in `plot_macrostate_composition`

## Description

## Changes

* `GPCCA.plot_macrostate_composition` now accepts soft (fractional) annotations in addition to hard categorical `adata.obs` columns. `key` becomes `str | Mapping[str, str]`:
  * `"week"` or `{"obs": "week"}` → categorical `adata.obs` column, **counts** per macrostate (unchanged behavior, y-axis "frequency").
  * `{"obsm": "cell_type"}` → a `adata.obsm` `DataFrame` of per-observation proportions (rows sum to 1); its columns become the stacked categories and each bar shows the **(weighted) mean composition** (y-axis "fraction").
* New `weight_key` argument (obsm-only) for a weight column in `adata.obs`, e.g. `weight_key="n_cells"` to weight aggregated samples by their cell count. `None` weights every observation equally.

## New

* Support for plotting macrostate composition from `.obsm` proportion frames, e.g. cell-type fractions emitted by sample-aggregation workflows where each observation carries a distribution over categories rather than a single label.

## Notes for reviewers

* The `.obs` path is untouched and byte-identical — the existing image-comparison tests pass unmodified.
* Because the proportion rows sum to 1, both the unweighted mean and the cell-count-weighted mean also sum to 1, so bars stay equal-height with no extra rescaling; only the y-axis label switches ("frequency" → "fraction").
* Rows of the `.obsm` frame are validated to sum to 1 (`atol=1e-3`); clear errors are raised for a non-`DataFrame` obsm value, a missing key, an invalid `key` type/source, or `weight_key` used with an `.obs` source.
* Adds image-comparison tests (obsm, obsm-weighted, `{"obs": ...}`) with ground-truth figures, plus six error-path tests.

## Related issues

Closes #

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b8153223118`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.