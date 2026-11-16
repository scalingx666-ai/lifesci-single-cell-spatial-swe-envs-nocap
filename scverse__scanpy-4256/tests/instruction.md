# Issue

**Title:** fix: use the non-zero median as `target_sum` on the sparse path

## Description

- [x]
- [x] Tests added

## Problem

With `target_sum=None`, `normalize_total` produces different results for sparse
and dense input when the matrix contains zero-count cells:

```python
x = np.array([[0.0, 0.0], [4.0, 6.0], [8.0, 12.0], [12.0, 18.0]])

# dense -> [ 0.  0.  8. 12.  8. 12.  8. 12.]
# csr   -> [ 0.  0.  6.  9.  6.  9.  6.  9.]
```

With enough empty cells the sparse result is worse than merely different. For
row sums `[0, 0, 10]` the median is 0, so the sparse path divides by zero and
returns an all-zero matrix, silently destroying the data.

## Cause

`_normalize_total_helper` picks the target sum in two places. The numba/CSR
branch uses `np.median(counts_per_cell)`, while the dense branch uses
`_compute_nnz_median`, which drops zero counts first. CSC is converted to CSR,
so it inherits the sparse rule.

This looks like an oversight rather than a deliberate difference.
`_compute_nnz_median` was the single shared code path until #3571 split the
function to add the numba branch, and the new branch got a plain median. The
existing `test_normalize_matrix_types` does compare dense against other array
types for `target_sum=None`, but it uses `pbmc68k_reduced()`, which has no
empty cells, so the divergence never showed up.

## Fix

Use `_compute_nnz_median` in the sparse branch too, so both paths agree. One
line.

## Test plan

- New `test_normalize_total_target_sum_ignores_zero_count_cells` in
  `tests/test_normalization.py`, parametrised over `ARRAY_TYPES`. It asserts the
  non-empty rows sum to the non-zero median (20, not 15) and that the result
  matches the dense path. It fails on main for the sparse types.
- `tests/test_normalization.py`: 204 passed, 81 skipped (200 passed before this
  change, plus the new cases).
- `ruff check` and `ruff format --check` clean at the pinned v0.15.20.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27bba90ce019`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.