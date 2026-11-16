# Issue

**Title:** Use Geary's C normality variance in spatial_autocorr

## Description

## Description

`squidpy.gr.spatial_autocorr` shares a single `_analytic_pval` implementation between `mode="moran"` and `mode="geary"`, swapping only `E[score]`. The variance it applies is the **Moran's I** normality variance (Cliff & Ord 1981); **Geary's C has a different normality variance**, so the analytic p-value (`pval_norm` / `var_norm`) for `mode="geary"` was miscalibrated.

.

## Fix

In `_analytic_pval`, branch on the statistic and use the Geary's C normality variance (matching `pysal/esda`'s `Geary`):

```
Var[C] = ((2·S1 + S2)(n − 1) − 4·S0²) / (2·(n + 1)·S0²)
```

Moran's I is left exactly as before.

## Verification

Reproduced with row-standardised 6-NN weights (the same setup as the issue):

| | squidpy `var_norm` (Geary) | esda `Geary.VC_norm` | ratio |
|---|---:|---:|---:|
| before | `1.4583e-03` | `1.7014e-03` | 0.857 |
| after  | `1.7014e-03` | `1.7014e-03` | 1.000 |

Computing the Geary closed-form from squidpy's **own** row-standardised weight moments reproduces the post-fix `var_norm` exactly (relative diff `0.0`), and it clearly differs from the old Moran value — confirming the previous code applied the wrong formula. The reporter's 100k-trial null study shows the analytic p-value going from badly non-uniform (KS p ≈ `1e-108`) to well-calibrated.

## Tests

Added `test_spatial_autocorr_var_norm_formula` (parametrised over `moran`/`geary`) asserting the emitted `var_norm` matches the closed-form variance of the chosen statistic. It passes with the fix and fails on the Geary case without it. All existing `spatial_autocorr` tests continue to pass; Moran's I output is unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55572c4c1942`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.