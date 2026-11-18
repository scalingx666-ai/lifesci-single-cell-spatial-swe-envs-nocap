# Issue

**Title:** simplify fun + cpdb null update

## Description

## 2.1.1 (08.11.2026)

### Changed

- `cellphonedb` now applies its zero rule (score 0 if the ligand or receptor mean is 0) to permuted data too, as CellPhoneDB does. Some `cellphone_pvals` of sparse interactions drop; `lr_means` are unchanged. On Kang et al. (2018) at `expr_prop=0`, agreement with CellPhoneDB 5.0.1 improves (p-value Spearman 0.991); at the default `expr_prop=0.1`, significance calls are practically unchanged.
- Internal: methods score through a single `MethodMeta(fun=...)` with signature `fun(x) -> (magnitude, specificity)`, where `x` maps `complex_cols` and `add_cols` to arrays; `combine=` and `observed_fn=` are removed. Other methods' results are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa65ec3c9b6c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.