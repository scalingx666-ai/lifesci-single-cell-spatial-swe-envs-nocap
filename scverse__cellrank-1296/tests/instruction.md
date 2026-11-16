# Issue

**Title:** Standardize optional dependency handling

## Description

Standardize how CellRank handles optional dependencies.

## Changes

### New helper: `_check_module_importable`

Adds `_utils/_import_utils.py` with a single helper that raises `ModuleNotFoundError` with actionable install instructions (pointing to the relevant `pip install cellrank[extra]`).

### Sites fixed

| Module | File | Before | After |
|--------|------|--------|-------|
| `moscot` | `_real_time_kernel.py` | Bare import — user sees raw `ModuleNotFoundError` | Guarded with `_check_module_importable("moscot", extra="moscot")` |
| `adjustText` | `_lineage_drivers.py` | `logg.error(...)` silently continues — broken plot, no traceback | Raises `ModuleNotFoundError` with `pip install cellrank[plot]` |
| `tqdm` | `_parallelize.py` | Triple fallback chain (`tqdm.auto` → `tqdm.std` → `None`) | Direct `from tqdm.auto import tqdm` — always available via scanpy |

### Sites intentionally left as-is

- **JAX** (`_similarity.py`): needs boolean-flag + stub pattern for conditional codepaths
- **PETSc/SLEPc** (`_linear_solver.py`): clean `_is_petsc_slepc_available()` helper
- **rpy2** (`_gamr_model.py`): well-structured `_maybe_import_r_lib()` with caching

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe4333116446`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.