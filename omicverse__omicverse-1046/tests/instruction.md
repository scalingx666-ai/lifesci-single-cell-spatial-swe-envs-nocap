# Issue

**Title:** storage='memory' + backend='cpp': threaded load, cuts and normalisation; implicit scaled layer

## Description

The in-memory path (`ov.read(path)`, the default) was very slow on large data: anndata copies the whole matrix single-threaded on every subset (twice per `_inplace_subset_*`), views re-slice the matrix on every `.X` access, and `scale` built a dense float64 matrix of all genes. SEA-AD MTG (1.38M cells, 7.6B nnz), Fig. 4 workflow, 64 threads:

| step | before | after |
|---|---|---|
| load | 30.3 s | 3.1 s |
| QC | 67.3 s | 9.4 s |
| normalisation + HVG | 109.5 s | 15.4 s |
| PCA | 17.6 s | 10.6 s |
| markers | 12.8 s | 3.1 s |
| **total (LocalMAP)** | **271 s** | **75 s** |
| peak memory | 370 GB | 196 GB |

Results are identical to master (obs/var, HVGs, residual variances, X, counts layer, X_pca compared on a 20k-cell SEA-AD subset).

## Changes (all only with `backend='cpp'` and an in-memory CSR `X`; everything else unchanged)
- `ov.read(storage='memory')`: CSR `X` read by anndataoom-fast on all threads (`read_csr`); falls back to `anndata.read_h5ad` without it, for non-CSR `X` or a `raw` section.
- `pp._qc.subset_inplace` / `subset_copy`: cut `X` and its CSR layers on all threads; anndata only cuts the metadata. All-true masks skip the cut. `subset_copy` leaves the input untouched (same semantics as `adata[mask].copy()`).
- QC: the QC filter plus the `min_genes` / `min_cells` filters become one cut (same cells/genes as the step-by-step subsets).
- `preprocess`: robust-gene subset in place (no view); the counts layer is copied once, after that cut.
- `normalize_total` row division, `log1p` (sparse, in place where the result replaces the input anyway) and the non-negative-integer check: threaded / one C++ pass, bit-identical.
- Pearson HVGs: no per-batch row/column views.
- `scale(use_implicit_centering=None)`: when the dense scaled matrix would exceed 32 GB (`OV_SCALE_DENSE_LIMIT_GB`), only per-gene `mean`/`std` are stored in `adata.var` (h5ad-writable) and `ov.pp.pca(layer='scaled')` builds exactly the HVG columns of the dense result — identical PCA. A message says so; `use_implicit_centering=False` forces the dense layer. `True` now also uses this (ddof=1, two-sided clip like the dense path) when the cpp backend is available.

Uses anndataoom-fast's new `memory` helpers (omicverse/anndataoom-fast#2); every call falls back to the previous code when they are missing.

## Tests
`tests/pp/test_inmemory_cpp.py`: threaded read == `anndata.read_h5ad`; subset helpers == anndata (input untouched); cpp QC keeps the same cells/genes as the python backend and does not filter the caller's object; implicit-scale PCA == dense PCA bit for bit and the result writes to h5ad. Related pp/others suites pass (failures only from missing optional packages).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5df522d0567f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.