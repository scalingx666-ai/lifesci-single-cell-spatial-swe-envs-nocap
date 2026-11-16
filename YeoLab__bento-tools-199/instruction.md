# Issue

**Title:** fix: support numpy 2, dask 2026 and spatialdata 0.7

## Description

Lets bento-tools install and run on numpy 2, scipy 1.17, dask 2026.1 and spatialdata 0.7. This is needed for a new Bento container image that clears the open Dependabot alerts in YeoLab/containers (pyarrow, distributed, fsspec, urllib3 can't be patched on the current RAPIDS 24.8 / spatialdata 0.2.3 stack).

. Should also help #190 and #177 (the scipy pin forced source builds of scipy 1.10).

## Dependency changes

- `scipy~=1.10.0` → `scipy>=1.10.0`. scipy 1.10 requires numpy <1.27 and Python <3.12; spatialdata 0.7 needs numpy 2.
- `decoupler>=1.7.0,<2.0`: decoupler 2.0 removed `dc.run_wsum` (#189).
- `xgboost>=2.0.3,<3.0`: xgboost 3 can't unpickle the bundled `rf_calib_20220514.pkl` ("Invalid serialization file").

## Code changes

- `bento/_utils.py`, `bento/tools/_shape_features.py`: update dask `.attrs` in place instead of assigning a new object. spatialdata 0.7 stores attrs in an accessor and assignment raised `'DataFrame' object has no attribute '_attrs'`.
- `bento/_utils.py`: only set `dataframe.query-planning: False` on dask < 2025. dask 2025.1 removed the legacy DataFrame and raises on import with that setting (seen in worker processes).
- `bento/tools/_colocation.py`: pass `shape` to `sparse.COO`; current sparse requires it.
- `bento/tools/_flux.py`: `drop(columns=list(old_cols))`; dask-expr evaluates the truthiness of a pandas `Index`.
- `bento/plotting/_multidimensional.py`: pass the plotted x/y to `adjust_text` instead of `objects=[scatter]`. That path gives adjustText NaN extents; scipy 1.10 let them into `KDTree`, scipy >= 1.11 raises "data must be finite". This is the "adjusttext kdtree compat" problem the scipy pin was added for.
- `tests/test_ut.py`: check `dd.DataFrame` instead of `dd.core.DataFrame`, which no longer exists.
- `tests/test_composition.py`: new `test_comp_plot_annotate` draws an annotated `bt.pl.comp` plot from the MERFISH sample. It fails with the KDTree error without the `adjust_text` fix.
- CI: run tests on every Ubuntu Python version. Before, only 3.10 ran tests, and 3.10 installs the old stack, so none of these breaks would have shown up.

## Verification

- Python 3.11.13 on macOS with numpy 2.2.6, scipy 1.17.1, pandas 2.3.3, spatialdata 0.7.3, dask/distributed 2026.1.1, zarr 3.1.6, decoupler 1.9.2, xgboost 2.1.4, adjustText 1.4.0: **29 passed**. Before these changes: 12 passed, 2 failed, 14 errors (plus the new comp-plot test failing).
- `flake8 --select=E9,F63,F7,F82`: 0 errors.
- **Not run locally on the old stack** (Python 3.10, spatialdata 0.2–0.5). CI's 3.10 job covers it; the changes are written to work with both (`.attrs.update` works on the legacy dask attrs dict too).

No version bump; release separately (e.g. 2.1.5).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e82209c19f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.