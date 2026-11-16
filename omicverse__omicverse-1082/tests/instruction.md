# Issue

**Title:** ov.vi.DRVI: native DRVI (replaces #1014, no drvi-py/scvi-tools)

## Description

Native PyTorch DRVI on ov.vi, replacing the scvi-tools/drvi-py adapter proposed in #1014 by @hurry060215-tech (credited as co-author; same public name `ov.single.drvi`).

- `ov.vi.DRVI`: split latent, per-dimension embedding into a shared decoder MLP, log-sum-exp aggregation; pnb/nb/zinb/poisson likelihoods; interpretability helpers `latent_traverse` / `differential_vars` / `dimension_gene_effects`.
- Runs on in-memory AnnData, AnnDataOOM and Dask (ELBO within 1% across the three).
- Validation vs drvi-py 0.2.8 (NeurIPS 2021 BMMC, 27,423 cells, 2000 HVG, 3 seeds, H100): ELBO 810.5±0.9 vs 810.2±2.0; NMI 0.797 vs 0.789; ARI 0.777 vs 0.743; disentanglement MSAS/LMS 0.227/0.203 vs 0.229/0.204; 60 s vs 628 s (~10×). Details: `benchmarks/vi/results_drvi.md`.
- Not ported: drvi-py's full `make_traverse_adata` grid, non-one-hot covariate embeddings.
- tests/vi: 56 passed, 1 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc512ac5a990`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.