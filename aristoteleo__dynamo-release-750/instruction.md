# Issue

**Title:** Add PFlog1pPF (BHGP 2022) depth normalization

## Description

## Summary

Integrates the depth-normalization method of Booeshaghi, Hjörleifsson, Gehring & Pachter (2022) — [pachterlab/BHGP_2022](https://github.com/pachterlab/BHGP_2022) — into dynamo's preprocessing: **PFlog1pPF** = proportional fitting → `log1p` → proportional fitting.

Unlike a single library-size normalization, the trailing PF corrects the depth distortion that `log1p` re-introduces; and unlike CLR-style per-cell centering, PFlog1pPF **stays sparse** (PF is a per-cell rescale, `log1p` preserves zeros).

## Changes

- **`normalization.py`** — new `proportional_fitting(mat, target_sum=None)` primitive (sparse/dense; scales each cell to a common depth, default mean depth; safely handles empty cells).
- **`transform.py`** — new `pflog1ppf` transform family (`pflog1ppf` / `pflog1ppf_adata_layer` / `pflog1ppf_inplace`), built like the existing `log1p` family so it is a drop-in `norm_method`. Sets `adata.uns["pp"]["X_norm_method"] = "pflog1ppf"`.
- **`Preprocessor.py`** — new `config_pflog1ppf_recipe` / `preprocess_adata_pflog1ppf` and a `"pflog1ppf"` recipe option. `adata.X` is normalized with PFlog1pPF, while spliced/unspliced layers keep the size-factor normalization required by downstream RNA velocity / vector field analyses.
- **`__init__.py`** — exports `proportional_fitting`, `pflog1ppf`, `pflog1ppf_adata_layer`.

## Usage

```python
import dynamo as dyn
p = dyn.pp.Preprocessor()
p.preprocess_adata(adata, recipe="pflog1ppf")   # full recipe
dyn.pp.pflog1ppf(adata)                          # or the transform on raw counts (stays sparse)
```

## Validation

- Numerically verified against the reference BHGP `pf()` implementation (sparse and dense paths agree; output stays sparse; equal final depth; empty cells stay zero).
- End-to-end test through the dynamo velocity pipeline (preprocess → dynamics → reduceDimension → cell_velocities) on pancreatic endocrinogenesis: the recipe runs cleanly and reduces residual depth dependence of the embedding (|corr(PC1, depth)| ≈ 0.45 vs ≈ 0.49 for library-size + log1p).

A companion tutorial PR adds a worked example to `dynamo-tutorials/100_tutorial_preprocess.ipynb`.

Reference: A. Sina Booeshaghi, Ingileif B. Hjörleifsson, Lambda Moses, Lior Pachter. *Depth normalization for single-cell genomics count data.* bioRxiv (2022). https://doi.org/10.1101/2022.05.06.490859

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01AD7gAdxa3Zt5uiQVDoANa5

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7d977a2831e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.