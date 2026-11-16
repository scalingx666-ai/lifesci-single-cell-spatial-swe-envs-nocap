# Issue

**Title:** feat(batch_correction): scvi kwarg-split helper + add scANVI / totalVI / scPoli backends

## Description

## Summary

Two layered changes in this PR:

**1. Kwarg routing fix for the scvi-family path** (commit `c3ccefce`)
`ov.single.batch_correction(methods='scVI', **kwargs)` historically forwarded everything to `scvi.model.SCVI.__init__` and called `model.train()` with no args. Train-side knobs (`max_epochs`, `batch_size`, `accelerator`, …) were silently misrouted or dropped. Adds `_split_kwargs_by_signature(kwargs, *(label, fn))` — a generic, signature-introspection-based partitioner — and uses it to route kwargs to the right destination.

**2. Three new integration backends** (commit `867a8a80`) — all reusing the helper:

| methods= | Backend | New required arg | Optional dep |
|---|---|---|---|
| `'scANVI'` / `'SCANVI'` | scvi-tools semi-supervised VAE | `labels_key=` (+ `unlabeled_category=`, default `'Unknown'`) | scvi-tools |
| `'totalVI'` / `'TOTALVI'` | scvi-tools joint RNA + protein VAE | `protein_expression_obsm_key=` | scvi-tools |
| `'scPoli'` / `'SCPOLI'` | scArches conditional VAE with per-condition prototypes | (optional) `cell_type_keys=` for prototype learning | scArches |

All three: write to `adata.obsm['X_<method>']`, raise `ImportError` with install hint when the optional dep is missing, are registered in `_BATCH_OBSM` so the `tracked` decorator's diagnostic viz picks up the right embedding key, and inherit the existing OOM-safety branch.

scANVI also writes predicted labels for unlabeled cells to `adata.obs['scANVI_predicted_labels']` (best-effort; silent on failure).

## Usage

```python
import omicverse as ov

# scVI (now with working train-side kwargs)
ov.single.batch_correction(
    adata, batch_key="batch", methods="scVI",
    n_latent=20, max_epochs=100, batch_size=512, early_stopping=True,
)

# scANVI (semi-supervised)
ov.single.batch_correction(
    adata, batch_key="batch", methods="scANVI",
    labels_key="celltype", unlabeled_category="Unknown",
    n_latent=20, max_epochs=100,
)

# totalVI (CITE-seq joint)
adata.obsm["protein_counts"] = adt_counts  # (n_cells, n_proteins)
ov.single.batch_correction(
    adata, batch_key="batch", methods="totalVI",
    protein_expression_obsm_key="protein_counts",
    n_latent=20, max_epochs=100,
)

# scPoli (conditional VAE with prototype-based label transfer)
ov.single.batch_correction(
    adata, batch_key="batch", methods="scPoli",
    cell_type_keys="celltype",
    embedding_dims=5, n_epochs=50, pretraining_epochs=40,
)
```

## Test plan

Two test files:

- `tests/single/test_kwargs_split.py` — 9 unit tests for the helper (synthetic callables, no scvi dep; CI-runnable). Covers exact match, multi-match collision + warning, fallthrough to `**kwargs`, drop + warning for fully unrecognised, order preservation, un-introspectable callables, and a `pytest.importorskip("scvi")`-gated real-scvi integration check.
- `tests/test_single_batch_scvi_family.py` — end-to-end smoke tests for scVI / scANVI / totalVI / scPoli on tiny synthetic AnnData (max_epochs=1 to keep runtime ≈55s for all 6 tests). Each test is `pytest.importorskip`-gated on its backend, so CI without scvi-tools simply skips.

Locally on omicdev (scvi-tools 1.3.0; scArches not installable due to tensorstore wheel build issues on manylinux):
- `test_kwargs_split.py`: **9/9 pass**
- `test_single_batch_scvi_family.py`: **5 passed, 1 skipped** (scPoli skipped, scarches missing locally)
- flake8 CI gate (`--select=E9,F63,F7`): clean

## Survey of other batch-correction algorithms

The omicverse-supported set after this PR: `harmony`, `combat`, `scanorama`, `scVI`, `scANVI`, `totalVI`, `scPoli`, `CellANOVA`, `Concord`, `seurat-CCA`.

Algorithms worth adding in follow-up PRs (with a one-line characterisation so a downstream PR can decide):

| Algorithm | Family | One-liner |
|---|---|---|
| BBKNN | KNN-graph rewiring | Drop-in graph fix, no training, very fast |
| fastMNN / mnnCorrect | Mutual nearest neighbours | Alternative MNN backend to Scanorama |
| pyliger | NMF | Python port of LIGER (iNMF), well-cited |
| scGen / trVAE | label-aware VAE | Treatment-response integration |
| DESC | deep embedded clustering | Integration via clustering pull |
| SAUCIE | autoencoder | Batch + denoising in one pass |
| MultiVI / PEAKVI | scvi-tools | Multimodal / ATAC-only — would belong under joint integration rather than RNA batch correction |

References that informed the scope:

- [Luecken et al., Nature Methods 2022 — scIB benchmark](https://www.nature.com/articles/s41592-021-01336-8) — the canonical comparison covering scVI / scANVI / Harmony / Scanorama / BBKNN / LIGER / fastMNN / ComBat.
- [scIB-E (2024 biorXiv)](https://www.biorxiv.org/content/10.1101/2024.12.09.627450) — extension benchmarking 16 deep-learning methods.
- [scvi-tools docs](https://docs.scvi-tools.org/) — for SCANVI / TOTALVI API surface.
- [scArches docs](https://docs.scarches.org/) — for the scPoli `(condition_keys, cell_type_keys)` API used here.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b87a7d8bd113`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.