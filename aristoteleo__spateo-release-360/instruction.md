# Issue

**Title:** Fix installation/dependency issue

## Description

## Summary
This PR focuses on installation compatibility and import stability, especially for Python 3.9–3.12 and newer `anndata` versions.

## What Changed
- Updated dependency constraints in `requirements.txt` with Python-version markers:
  - `anndata`, `numpy`, `pandas`, `scipy`, `Shapely`, `h5py`, `setuptools`.
- Improved `setup.py` requirements parsing:
  - Ignore empty/comment lines when loading requirements.
  - Updated classifiers to include Python 3.11/3.12 and removed outdated 3.7 classifier.
- Added compatibility handling for `anndata` API changes in `spateo/data_io.py`:
  - Fallback imports for `read*` functions between older and newer `anndata` versions.
- Reduced circular import risk by moving heavy imports to lazy/runtime import:
  - `spateo/plotting/static/three_d_plot/align_plots.py`
  - `spateo/plotting/static/three_d_plot/three_dims_plots.py`
  - `spateo/tdr/interpolations/utils.py`
- Fixed import path for alignment utility:
  - `get_optimal_mapping_relationship` now imported from `spateo.alignment.utils`.
- Added optional behavior for trajectory model output in morphopath:
  - New parameter `return_merged` in `construct_trajectory_X` and `construct_trajectory` (default `True` to keep existing behavior).

## Why
- Resolve installation issues across Python versions.
- Handle upstream library API changes (`anndata`) without breaking existing workflows.
- Avoid circular-import related initialization/runtime failures.
- Provide more flexible trajectory model output format for downstream usage.

## Backward Compatibility
- Default behavior remains unchanged (`return_merged=True`).
- Existing call sites should continue to work without modification.

## Validation
Local install checks passed in fresh conda envs:
- Python 3.9 / 3.10 / 3.11 / 3.12
- `pip install .` succeeded
- `pip check` succeeded
- `import spateo` succeeded

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ce1a90128a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.