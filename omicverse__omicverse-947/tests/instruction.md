# Issue

**Title:** fix(sude): correct torch diag gradient to avoid NaN embedding

## Description

## Root cause
In `_learning_s_torch`, the gradient used `torch.diag` twice:

```python
diag_sum = torch.diag(torch.sum(ProMatY, dim=0))
grad = (torch.diag(diag_sum) - ProMatY) @ Y_torch
```

The second `torch.diag` turns the diagonal matrix back into a vector, so the subsequent subtraction broadcasts incorrectly and the embedding diverges to NaN. `opt_scale` then calls `NearestNeighbors.fit` on the NaN embedding, producing the error reported in the issue.

## Fix
Keep the diagonal matrix construction matching the CPU reference:

```python
diag_sum = torch.sum(ProMatY, dim=0)
grad = (torch.diag(diag_sum) - ProMatY) @ Y_torch
```

## Verification
- Reproduced on real `pbmc3k_raw.h5ad` through `preprocess -> scale -> pca -> sude` in `cpu-gpu-mixed` mode.
- Before: Torch `learning_s` returns all-NaN landmarks (1806/1806 NaN for 903 landmarks x 2 dims).
- After: full `ov.pp.sude(adata, use_rep='scaled|original|X_pca')` returns `(2700, 2)` with 0 NaN / 0 Inf.

## Also included in this PR
- Stop `complexheatmap` from mutating global `matplotlib.rcParams`; it no longer calls the global `plot_set` helper.
- Scope the `plot_set` smoke test with `matplotlib.rc_context()` and assert `complexheatmap` leaves `figure.dpi` unchanged.
- Add the missing `matplotlib-venn` test dependency and update the venn smoke test to the current `return ax` behavior.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c30f9a6ef7a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.