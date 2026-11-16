# Issue

**Title:** fix(pp): qc_gpu doublet methods (scdblfinder/etc.) fail on the GPU matrix

## Description

## Summary

. In GPU mode, `ov.pp.qc(..., doublets_method='scdblfinder')` (the default) crashes with:

```
Length of values (13503) does not match length of index (2695)
```

`13503` ≈ n_genes, `2695` ≈ n_cells.

### Root cause

`qc_gpu` moves the matrix to the GPU (cupy) via `rsc.get.anndata_to_GPU`. **scrublet** runs there natively (rapids-singlecell), so it works — but the other doublet backends are **CPU / NumPy** tools:

- `scdblfinder` → `pyscdblfinder`
- `doubletfinder` → `pydoubletfinder`
- `sccomposite`

Handed a **cupy** matrix, `scipy.sparse.issparse(X)` is `False`, so they misread its orientation and compute one value **per gene**. Writing that back onto the (cells-indexed) `obs` raises the length mismatch. That's why "only `doublets_method='scrublet'` works in GPU mode".

### Fix

Move the matrix back to host memory (`rsc.get.anndata_to_CPU`) before any **non-scrublet** doublet method, so the GPU path matches the already-correct CPU path. scrublet still runs on the GPU.

```python
if doublets_method != 'scrublet':
    rsc.get.anndata_to_CPU(adata)
```

### Note on testing

The GPU path needs `rapids-singlecell` + `cupy` + a GPU, which aren't available in CI, so this can't be exercised by an automated test here. The change is a one-line host-memory transfer that makes the GPU doublet path identical to the working CPU path (where these NumPy tools already run correctly).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `854ff6a1c22d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.