# Issue

**Title:** fix: raise a clear error when log2FC has no cells to compare against

## Description

`_calc_log2fc` splits cells into `subject` (the current group) vs `rest` (everything else), then computes `rest.layers['normcounts'].mean(0)`. If a `sample_key` group happens to contain only one `groupby` category, `rest` ends up with 0 rows, and scipy's sparse `mean()` divides by that empty shape, surfacing as a bare `ZeroDivisionError` deep in scipy internals with no useful context, exactly matching the traceback in the issue and nrclaudio's later diagnosis in the same thread.

Raises a `ValueError` explaining the actual cause (no cells left to compare against, usually a `sample_key`/`groupby` combination issue) instead of letting scipy's error leak through.

### Testing

Added `test_calc_log2fc_no_rest_raises`, which reproduces the empty-rest condition directly against the existing `pbmc68k_reduced` fixture. `tests/test_liana_pipe.py` (6/6), `tests/test_rank_aggregate.py` + `tests/test_sc_methods.py` (20/20, includes `by_sample` and mdata paths) all pass in a fresh Python 3.12 container.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `705bcf9dd9fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.