# Issue

**Title:** feat(space): integrate SPLIT purification workflow

## Description

## Summary

Integrate [py-SPLIT](https://github.com/omicverse/py-SPLIT) into `omicverse.space`, exposing an AnnData-native SPLIT purification workflow for spatial transcriptomics.

This follows the same reconstruction flow as #825: the standalone `py-*` package is developed first, then the core workflow is exposed through the main `omicverse` API with targeted tests.

## What's added

### `omicverse/space/_split.py` (new)
- `split_purify()` - default SPLIT-style purification from generic deconvolution weights and reference profiles
- `split_spatial_score()` - neighborhood primary/secondary type support scores for spatially aware selective purification
- `split_balance()` - raw/purified balancing with optional spot-class handling and SPLIT-shift metadata swaps
- `split_reassign_residuals()` - residual transcript reassignment to spatial neighbors with mass accounting in `adata.uns['split_residual_stats']`
- Dense/sparse support, label-based alignment, reference orientation handling, and input validation

### `omicverse/space/__init__.py` (modified)
- Exposes `ov.space.split_purify`, `split_spatial_score`, `split_balance`, and `split_reassign_residuals`

### `tests/space/test_split.py` (new, 9 tests)
- Formula parity, sparse input, primary inference, copy mode, selective purification
- Spatial scoring, balance, SPLIT-shift, residual reassignment, biological sanity
- Invalid input rejection

## Usage

```python
import omicverse as ov

ov.space.split_purify(adata, weights, reference, primary_cell_type=adata.obs['cell_type'])
ov.space.split_spatial_score(adata, weights, adata.obs['first_type'], secondary_cell_type=adata.obs['second_type'])
ov.space.split_balance(adata, threshold=0.15)
ov.space.split_reassign_residuals(adata, mode='count_proportional')
```

## Result parity

The implementation mirrors the standalone `py-SPLIT` package and is verified against an explicit SPLIT formula fixture. The standalone package currently has 29 tests; this PR adds main `omicverse` API coverage with 9 targeted tests.

## Test plan

- [x] `python -c "import omicverse as ov; print(ov.space.split_purify.__name__)"` resolves
- [x] `python -m py_compile omicverse/space/_split.py`
- [x] `pytest tests/space/test_split.py -q` - 9/9 pass

## Notes

- No R runtime code is included.
- No new dependency is required beyond existing `omicverse` dependencies.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbca54e27e24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.