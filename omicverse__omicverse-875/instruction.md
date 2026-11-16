# Issue

**Title:** fix(wgcna): restore SciPy 1.18 compatibility and serialization

## Description

## Summary

.

The PyWGCNA tutorial workflow could fail at multiple consecutive stages with SciPy 1.18:

1. `calculate_dynamicMods()` used floating-point ordinal ranks as NumPy indices, raising an `IndexError`.
2. After casting the first rank array, floating-point module labels propagated into `labels2colors()`, whose categorical branch created an ndarray but continued to access it through the DataFrame-only `.Value` attribute.
3. `saveWGCNA()` failed with a `PicklingError` because `register_function` replaced decorated classes with function wrappers, so the instance class no longer matched the class exposed under its module-qualified name.

This PR fixes the complete failure chain and adds deterministic regression coverage for dynamic module detection, label conversion, and WGCNA serialization.

## Root cause

SciPy 1.18 returns floating-point arrays from `scipy.stats.rankdata(..., method="ordinal")`. The dynamic-tree implementations assumed that these ranks were always integer arrays and used them directly for indexing and module-label construction.

The resulting integral floating-point labels entered the categorical branch of `labels2colors()`. That branch assigned `Categorical.codes`, an ndarray, to `nLabels`, while the remaining code still expected a DataFrame with a `Value` column.

Separately, the registry decorator registered the original class but returned a function wrapper. Pickle resolves classes through their module and class name, so instances of the original class could not be matched to the wrapper stored under `omicverse.external.PyWGCNA.wgcna.pyWGCNA`.

## Changes

- Convert ordinal rank results to `np.intp` before they are used as array indices or module labels.
- Apply the rank conversion consistently in both the canonical bulk dynamic-tree implementation and the mirrored PyWGCNA implementation.
- Normalize DataFrame, Series, and array-like label inputs to a one-dimensional array in `labels2colors()`.
- Preserve integral floating-point module labels as numeric labels instead of incorrectly converting them through categorical codes.
- Use a consistent ndarray-based path for label bounds, missing values, and color lookup.
- Extend repeated color sequences when the highest label equals the original sequence length, preventing an off-by-one index error at the palette boundary.
- Preserve decorated classes as classes in `register_function` while retaining their registry metadata. Existing function-decoration behavior is unchanged.
- Add regression tests for SciPy 1.18-style floating-point ordinal ranks, integral floating-point module labels, and public `saveWGCNA()`/`readWGCNA()` round-trip serialization.

## Results

- Dynamic module detection accepts SciPy 1.18 ordinal rank output without invalid NumPy indexing.
- Generated module labels retain an integer dtype.
- `labels2colors()` converts the reported floating-point labels without raising `AttributeError`.
- Color-sequence extension handles labels exactly at the palette-length boundary without indexing past the original sequence.
- Public `ov.bulk.pyWGCNA` remains a class.
- WGCNA objects can be saved and loaded through the documented public API.

## Validation

- Exact compatibility environment: Python 3.12, NumPy 2.2.6, SciPy 1.18.0, and Pandas 2.3.3: `3 passed`.
- Bulk, lazy WGCNA wiring, and registry class tests: `83 passed, 1 skipped`.
- Independent subagent review: no blocking findings; `90 passed` across focused WGCNA, registry, and MCP class tests.
- `git diff --check`.

Five unrelated cases in `tests/bulk/test_deg_backends.py` require the optional `pydeseq2` dependency, which was not installed in the local development environment. All other selected bulk tests passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3777a62fb8a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.