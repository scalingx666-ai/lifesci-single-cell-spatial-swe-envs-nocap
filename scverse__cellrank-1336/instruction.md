# Issue

**Title:** feat(estimators): support omitting missing values in lineage drivers

## Description

## Description

.

That issue asked why CellRank doesn't use `scipy.stats.pearsonr` for lineage-driver correlations (answer, from the maintainers: performance — scipy doesn't vectorize many pairwise correlations well). The reporter then asked for the one scipy feature they were missing: **support for missing values**, since patient-level pseudobulk data can have `NaN`s when a sample lacks a given cell type.

This PR adds a `nan_policy` argument to `compute_lineage_drivers` (and the underlying `_correlation_test` / `_correlation_test_helper`), mirroring `scipy.stats.pearsonr`:

- `nan_policy="propagate"` (default) — unchanged behavior.
- `nan_policy="omit"` — each gene/lineage correlation is computed only over the cells where **both** entries are non-missing.

## Implementation

The omit path (`_mat_mat_corr_dense_omit_nan`) is implemented with masked matrix multiplications, so it keeps the fast vectorized behavior that motivated not using scipy in the first place (a handful of matmuls instead of one, rather than a Python loop over pairs). It uses the same population-std / `(n - 1)` convention as `_mat_mat_corr_dense`, so it **reproduces the existing dense result exactly when no values are missing** (verified to machine precision), and it threads a per-pair sample size `n` into the Fisher transformation so the degrees of freedom are correct for each pair.

### Scope / guardrails (per discussion)

- Supported for **dense** expression data and **`method="fisher"`** only.
- Sparse input + `"omit"` → clear `NotImplementedError` (suggests densifying).
- `method="perm_test"` + `"omit"` → clear `NotImplementedError`.
- Invalid `nan_policy` → `ValueError`.

## Tests

Added to `tests/test_lineage_drivers.py`:
- `omit` == `propagate` when there are no NaNs (allclose).
- `omit` recovers finite, in-`[-1, 1]` correlations when NaNs are present (where `propagate` makes everything NaN).
- sparse + omit, perm_test + omit, and invalid policy all raise.

Also independently verified that `_mat_mat_corr_dense_omit_nan` matches `scipy.stats.pearsonr(nan_policy="omit")` to ~1e-16 (modulo CellRank's existing `n/(n-1)` scaling convention), with exact per-pair counts.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3931cc88e82d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.