# Issue

**Title:** feat(space): add SPATA2-inspired AnnData spatial utilities

## Description

## Summary

Adds an initial AnnData-native spatial helper layer inspired by SPATA2 coordinate, variable, outline, outlier, and unit-conversion workflows. This is intentionally scoped as small OmicVerse spatial utility coverage, not a complete SPATA2 or py-SPATA2 parity claim.

## Changes

- Adds `omicverse/space/_spata2.py` and exports the helper functions through `ov.space`.
- Provides coordinate extraction, variable joins, convex-hull tissue outlines, spatial outlier detection/removal, and explicit pixel/unit conversion.
- Handles common `adata.obs` name collisions when `spata2_get_coords(include_obs=True)` is used with existing `barcode`, `x`, or `y` columns.
- Aligns `spata2_tissue_outline_source_obs` with the returned outline vertices rather than all unique coordinates.
- Rejects ambiguous `layer=...` plus `use_raw=True` extraction.
- Expands focused tests for collision handling, outline source alignment, and raw/layer boundary behavior.

## Validation

- `D:\Anaconda3\envs\omicverse\python.exe -m pytest tests\space\test_spata2.py -q` -> 11 passed, 6 warnings
- `D:\Anaconda3\envs\omicverse\python.exe -m py_compile omicverse\space\_spata2.py omicverse\space\__init__.py`
- `git diff --check`

## Scope note

This PR should be reviewed as an initial AnnData spatial utility slice inspired by SPATA2 workflows. Full SPATA2 namespace parity remains tracked separately in `omicverse/py-SPATA2` and should not be inferred from this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d04c08f1e0d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.