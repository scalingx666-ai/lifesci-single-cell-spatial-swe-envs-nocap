# Issue

**Title:** Bump dependency lower bounds + add optional extras

## Description

## Summary

Aggressive dependency lower bounds bump targeting numpy 2+ / modern ecosystem, plus user-facing optional extras.

## Changes

### Dependency lower bounds (6b)

| Package | Before | After | Rationale |
|---------|--------|-------|-----------|
| `anndata` | `>=0.9` | `>=0.11` | numpy 2 compat |
| `joblib` | `>=0.13.1` | `>=1.4` | first with py3.12 classifier |
| `matplotlib` | `>=3.5` | `>=3.9` | full numpy 2 support |
| `networkx` | `>=2.2` | `>=3.4` | modern |
| `numba` | `>=0.51,!=0.57` | `>=0.60` | first with numpy 2 |
| `numpy` | `>=1.22` | `>=2` | scanpy 1.12 requires it; our tests already use 2.3 |
| `pandas` | `>=1.5` | `>=2.2` | modern (can't go to 3.x — anndata caps `<3`) |
| `scanpy` | `>=1.7.2` | `>=1.11` | numpy 2 support |
| `scipy` | `>=1.12` | `>=1.14` | first with full numpy 2 support |
| `scvelo` | `>=0.2.5` | `>=0.3` | latest line |
| `seaborn` | `>=0.10` | `>=0.13` | first with py3.12 classifier |
| `wrapt` | `>=1.12.1` | `>=1.16` | first with cp312 wheels |

Unchanged: `docrep>=0.3` (unmaintained, pure Python), `pygam>=0.10`, `pygpcca>=1.0.4` (bump after upstream PRs), `scikit-learn>=1.6`.

### Test deps

| Package | Before | After |
|---------|--------|-------|
| `igraph` | unpinned | `>=1` |
| `leidenalg` | unpinned | `>=0.11` |
| `pillow` | unpinned | `>=10` |
| `pytest-cov` | `>=4` | `>=6` |
| `pytest-mock` | `>=3.5` | `>=3.14` |

### Docs deps

| Package | Before | After |
|---------|--------|-------|
| `furo` | `>=2022.9.29` | `>=2024.8.6` |
| `myst-nb` | `>=0.17.1` | `>=1.2` |
| `sphinx` | `>=5.1.1` | `>=7.4` |
| `sphinx-autodoc-typehints` | `>=1.10.3` | `>=2.5` |
| `sphinx-design` | `>=0.3` | `>=0.6` |
| `sphinx-tippy` | `>=0.4.1` | `>=0.4.3` |
| `sphinxcontrib-bibtex` | `>=2.3` | `>=2.6` |
| `sphinxcontrib-spelling` | `>=7.6.2` | `>=8` |

### Optional extras (6a)

| Extra | Packages | Use case |
|-------|----------|----------|
| `jax` | `jax`, `jaxlib` | VelocityKernel stochastic mode |
| `moscot` | `moscot` | RealTimeKernel.from_moscot() |
| `petsc` | `mpi4py`, `petsc4py`, `slepc4py` | Large-scale Schur decomposition |
| `plot` | `adjustText` | Label placement in lineage drivers |
| `r` | `rpy2>=3.3` | GAMR model (R's mgcv) |

### pygpcca jinja2 override

`pygpcca==1.0.4` incorrectly pins `jinja2==3.0.3`, conflicting with `sphinx>=7.4` (requires `jinja2>=3.1`). Added `[tool.uv] override-dependencies` to unblock. Will remove once pygpcca releases a fix.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bdbf1ecc89a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.