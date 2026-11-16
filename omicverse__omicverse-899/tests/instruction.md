# Issue

**Title:** feat(single): add Seurat-style RPCA integration (methods='rpca')

## Description

## Summary

Implements #883 — a Python function for **RPCA (reciprocal PCA) batch integration**, equivalent to Seurat's `IntegrateLayers(method = RPCAIntegration, ...)`, so users can run it directly on `AnnData` without switching to R.

```python
import omicverse as ov
# unified dispatcher
ov.single.batch_correction(adata, batch_key='batch', methods='rpca')
# or directly
ov.single.rpca_integrate(adata, 'batch', n_pcs=30, reference='ctrl')
# → adata.obsm['X_rpca']
```

## What it does

A **faithful, function-for-function port** of Seurat v5's
`FindIntegrationAnchors(reduction = "rpca")` + `IntegrateEmbeddings` (new module `omicverse/single/_rpca.py`, pure numpy/scipy/scikit-learn, no R / rpy2):

1. Per-batch `ScaleData` (clip 10) + `RunPCA`.
2. `ReciprocalProject` — project each batch onto the other's PCA loadings; column-scale + per-cell L2.
3. Exact **mutual nearest neighbor** anchors across the reciprocal spaces (`FindNN` → `FindAnchorPairs`).
4. Shared-neighborhood **anchor scoring** with percentile rescaling (`ScoreAnchors`).
5. Gaussian-kernel **anchor weighting** (`FindWeights`/`FindWeightsC`, `w = 1 − exp(−dist'·score·sd²/4)`, column-normalized) and the batch-vector correction `corrected = query − Wᵀ·integration_matrix` (`IntegrateDataC`), applied to the original joint PCA (Seurat `orig.reduction`).
6. hclust anchor-count **sample tree** for >2 batches (`BuildSampleTree`).

Surfaced via `ov.single.batch_correction(methods='rpca' | 'seurat_rpca')` and exported as `ov.single.rpca_integrate`. Accepts `features=`, `reference=`, `k_anchor=`, `k_score=`, `k_weight=`, `sd_weight=`, `orig_rep=`.

## R-parity validation (Seurat 5.4.0)

Validated on **real data** — two RCC patient samples from a public kidney atlas (2.4k cells, genuine cross-sample batch effect). Feeding the port and Seurat identical per-batch PCA + integration features + joint PCA (both run with exact `nn.method="rann"`):

| metric | result |
|---|---|
| anchor set | **identical** — 849 pairs (Seurat reports 1698 = 849 mirrored) |
| `integrated.dr` flatten Pearson | **0.99995** |
| per-PC Pearson | min 0.9995, median 0.99992 |
| relative Frobenius error | 1.0% |

The residual comes from neighbor-tie ordering in the weight kNN; the anchor graph and correction are numerically equivalent to Seurat.

## Tests

`tests/test_single_rpca.py` (scanpy/sklearn-guarded): runs end-to-end, removes a synthetic batch shift (mixing ↑ vs raw PCA), the dispatcher path, determinism, and the >2-batch sample-tree path. **5 passed**; `flake8 --select=E9,F63,F7` clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa4013978511`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.