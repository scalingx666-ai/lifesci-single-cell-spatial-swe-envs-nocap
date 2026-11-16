# Issue

**Title:** fix(genetics): normalize sparse gsMap inputs

## Description

## Summary

Makes gsMap count normalization work with both dense and sparse AnnData matrices.

## Changes

- Removes the unavailable Scanpy private API check.
- Uses the matrix max() method instead of converting sparse matrices with np.asarray.
- Preserves the existing normalization threshold and workflow.

## Validation

- 2 regression tests passed.
- Tests cover dense arrays and SciPy CSR matrices.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3777a62fb8a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.