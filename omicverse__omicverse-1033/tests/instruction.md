# Issue

**Title:** GPU mode on Dask row blocks + ov.read(storage='memory'|'disk')

## Description

## What
Two choices instead of three for running omicverse on large data:

```python
ov.settings.gpu_init()                          # where it is computed: cpu / cpu-gpu-mixed / gpu
adata = ov.read("x.h5ad", storage="disk")       # where the matrix lives: "memory" (default) / "disk"
```

| mode | `storage='memory'` | `storage='disk'` |
|---|---|---|
| cpu | AnnData in RAM | AnnDataOOM (anndataoom), streamed by the C++ kernels |
| cpu-gpu-mixed | AnnData in RAM | AnnDataOOM; PCA/kNN/UMAP on the GPU |
| gpu | AnnData in RAM → GPU (RAPIDS) | **new:** Dask row blocks streamed from disk to the GPU |

`ov.read(backend='python'|'rust')` keeps working with a `FutureWarning` (`'rust'` = AnnDataOOM as before). The CPU kernels (`backend='cpp'/'python'`) stay an advanced setting. MCP `read` schema exposes `storage`.

## New: chunked GPU mode (`omicverse/pp/_dask.py`)
In GPU mode `storage='disk'` keeps `X` as a Dask array of CSR row blocks (`chunk_size` cells, default 20,000) read with `preadv` through a fixed 64 MB pinned buffer per thread (compressed/chunked h5ad via anndataoom-fast's decoder). `qc`, `preprocess` (`shiftlog|pearson`), `scale`, `pca` and `find_markers(method='cosg')` stream the blocks, so the matrix never has to fit in GPU or host memory:
- one-pass QC metrics and gene filtering (CUDA kernels, float64 atomics)
- lazy `normalize_total`/`log1p` that build new blocks (the `counts` layer is untouched)
- Pearson-residual HVGs: zero-count residuals summed by a fused reduction, stored counts corrected per entry; per batch like rapids-singlecell / scanpy
- per-gene statistics cached by Dask name so filtering, robust genes, HVGs and scaling share passes: the matrix is read 4 times up to PCA (+1 for markers)
- PCA by covariance eigendecomposition with the scaled HVG columns persisted on the device (sklearn sign convention)
- COSG group statistics through anndataoom-fast 0.1.3 (dependency bumped)
- `ov.settings.gpu_init(dask=True)` starts a `LocalCUDACluster` for multi-GPU runs (not tested on >1 GPU yet)

Not supported on a Dask X (clear errors): doublet detection (`qc(doublets=False)`), `pearson|*` / `*|seurat` preprocess, `no_cc`, `exclude_highly_expressed`, non-COSG markers.

## Results
- lung200k: same cells/genes as the in-memory CPU path, identical QC metrics, HVGs 2000/2000, residual variances rel. err. 5e-6, PCs |r| = 1.0
- SEA-AD MTG (1.38M cells, 7.6B nnz, 91 GB h5ad), one H100, warm page cache: the whole Fig. 4 workflow (QC → markers) in **55 s with 5 GB peak host memory**; brisc 93 s / 114 GB and omicverse cpu 91 s / 13 GB (32-core AMD 9754); the in-memory RAPIDS path cannot load it (> 128 GB host RAM)

## Tests
`tests/pp/test_dask_mode.py` (16; CPU and GPU blocks, contiguous and gzip files, pass count = 4, counts layer unchanged, batch-aware HVG vs scanpy, storage resolution, deprecated alias). Full `tests/pp single others mcp utils` run: same failures as master (missing optional packages only).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9fa7af348700`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.