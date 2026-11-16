# Issue

**Title:** fix: handle zero counts in Pearson residual normalization

## Description

Pearson residual normalization currently produces `NaN` values for zero-count genes or cells because their fitted mean and variance are zero. An entirely zero matrix also divides by zero when constructing the fitted means. These values can make downstream PCA fail after subsetting the gene matrix.

This change assigns zero residuals by convention to zero-count cells/genes, including an all-zero input, while leaving positive-mean entries on the existing negative-binomial/Poisson formula. `np.divide(..., where=mu != 0)` avoids the invalid division rather than replacing arbitrary NaNs afterward. The docstring describes the convention.

- [x]
- [x] Tests included: 96 parameter combinations covering dense/CSR/CSC input, float32/int64 counts, finite/infinite theta, default/no clipping, and empty genes/cells/both/all; plus three storage-mode tests.
- Tests were added first: all 99 new cases failed on the original implementation with floating-point errors, then passed with the fix.
- A nonzero constant gene is included to check that it is not incorrectly zeroed merely because its raw variance is zero. Nonempty entries are compared against the independently calculated Pearson formula.
- Ruff lint and formatting checks pass.
- Full `tests/test_normalization.py`: **382 passed, 2 skipped** on Windows with Python 3.13.16, NumPy 2.5.3, and AnnData 0.13.4.
- A separate normalization-to-PCA smoke check with an empty cell and gene passed, preserving all four input cells.
- Verified the updated public docstring; the full documentation site was not built locally.

AI assistance: implementation, tests, and this description were prepared with OpenAI Codex. No independent human review is claimed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7ad567d9f7ca`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.