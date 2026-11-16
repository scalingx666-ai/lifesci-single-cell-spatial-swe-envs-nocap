# Issue

**Title:** fix(pl): restore plotting compatibility APIs

## Description

## Summary

Restores plotting compatibility for current SciPy, AnnData, and Matplotlib versions.

## Changes

- Replaces removed sparse-matrix .A access with .toarray() in plot_heatmap.
- Restores ov.pl.plot_ConvexHull and ov.pl.stacking_vol.
- Keeps legacy ov.utils entry points through deprecation-warning wrappers.
- Updates plotting registry examples and docstrings to use canonical ov.pl APIs.
- Fixes categorical palette handling for sequence inputs.
- Replaces the deprecated STT colormap accessor.
- Makes plotting wrapper tests isolate sys.modules correctly.

## Validation

- 1402 plotting, API, wrapper, and architecture tests passed.
- The real ov.utils.stacking_vol compatibility path is covered.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3777a62fb8a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.