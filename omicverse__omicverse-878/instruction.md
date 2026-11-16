# Issue

**Title:** fix: make FlowSig parallel bootstrapping process-safe

## Description

﻿## Root cause

FlowSig bootstrap workers received the complete `AnnData` object. Any unrelated non-picklable state in `adata.uns` could therefore break loky deserialization before network learning started.

## Fix

- extract the numeric flow matrix, condition masks, and spatial block indices once in the parent process
- pass only NumPy arrays and integer indices to loky workers
- use a per-bootstrap `numpy.random.default_rng(seed)` while retaining seeds `0..n_bootstraps-1`
- keep all `AnnData` mutation in the parent process and preserve the public API and result keys
- validate bootstrap counts, keys, conditions, blocks, row counts, and matrix shape early
- fix UT-IGSP non-spatial resampling and map filtered target indices back to the original flow variables
- add focused regression tests for spatial/non-spatial GSP and UT-IGSP, serial/process parity, zero-variance columns, and unpicklable `AnnData.uns` state
- update the tutorial submodule to omicverse/omicverse-tutorials#86

This PR intentionally does not change `pyproject.toml`, optional dependencies, or the existing GitHub Actions workflow.

## Validation

- 16 FlowSig network tests passed with real `causaldag`, including serial/process parity and deliberately unpicklable `AnnData.uns` state
- in the existing local OmicVerse environment: 14 passed, 2 skipped because `causaldag` is not installed
- `_network.py` compiles and `git diff --check` passes
- both tutorial notebooks pass `nbformat.validate()` and all code cells compile
- the repository's unchanged Python 3.10-3.12 workflow is running on the minimized diff

Until a release containing this fix is installed, `n_jobs=1` remains the workaround.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a507569490eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.