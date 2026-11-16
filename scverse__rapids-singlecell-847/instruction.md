# Issue

**Title:** Align Geary's C pval_norm with squidpy and run utag PCA implicitly

## Description

- spatial_autocorr: use Geary's C own normality variance (Cliff & Ord) for pval_norm, as squidpy does since 1.8.2, instead of Moran's I variance.
- calculate_niche(flavor="utag"): for sparse data, run the PCA on the implicit mean-centered operator D^-1 A X instead of materializing it. The smoothed matrix has ~mean-degree times the nnz of X; on Atera Xenium panels (18k genes) it failed in cuSPARSE (170k cells) or overflowed int32 and silently returned no features (718k cells). This also fixes failures on unexpressed genes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28a8264e8f35`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.