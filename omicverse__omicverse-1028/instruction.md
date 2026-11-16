# Issue

**Title:** GPU mode: work with any rapids-singlecell release (0.11 – 0.18)

## Description

omicverse's GPU (RAPIDS) mode was written against one rapids-singlecell (rsc) API. Several calls broke on other releases, and one was wrong on all of them.

New `omicverse/pp/_rsc_compat.py` wraps the calls whose API changed:

| call | change across rsc releases | wrapper |
|---|---|---|
| `pp.filter_cells` / `pp.filter_genes` | ≤ 0.11: `qc_var`/`min_count`, filters on a possibly stale `.obs`/`.var` column; ≥ 0.12: Scanpy arguments, one threshold per call | ≥ 0.12: one call per threshold; older: counts computed on the GPU, then filtered |
| `pp.normalize_total` | `exclude_highly_expressed`/`max_fraction` only from 0.14; `target_sum=None` = median including zero-count cells before 0.14, median of non-zero counts from 0.14 | older: Scanpy's highly-expressed exclusion computed on the GPU; always the non-zero median |
| `pp.pca` | `use_highly_variable` rejected from 0.17 | translated to `mask_var` |
| `pp.neighbors` | omicverse passed its connectivity `method` ('umap'/'gauss') as rsc's `algorithm` (the kNN search), which rsc ≥ 0.13 rejects | sent as rsc's `method` (≥ 0.14); a kNN algorithm name is still passed as `algorithm` |

`random_state` → `rng` (0.17) needs nothing, since rsc still accepts `random_state`.

**Tests:** `tests/pp/test_rsc_compat.py` compares against Scanpy on the GPU (same kept cells/genes, normalised values to float precision) and checks the argument translations.
- 13/13 pass with rsc 0.11.1, 0.12.7 and 0.13.4 (cuml 24.04), 0.14.1 (RAPIDS 25.08 container) and 0.16.1, 0.17.0, 0.18.1 (RAPIDS 26.10 container, built from source).
- The full GPU workflow (QC → preprocess → PCA → neighbors → Leiden at 5 resolutions → UMAP → COSG markers) runs on lung200k with rsc 0.14.1 and 0.18.1.
- The COSG step needs anndataoom-fast 0.1.2 (device arrays are copied to the host); the dependency bump will follow once it is on PyPI.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e1d3619e669`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.