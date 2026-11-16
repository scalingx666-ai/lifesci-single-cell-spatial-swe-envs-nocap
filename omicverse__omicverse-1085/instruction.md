# Issue

**Title:** ov.vi.MRVI: native MrVI (replaces #1009, no scvi-tools/jax)

## Description

Native PyTorch MrVI on ov.vi, replacing the scvi-tools adapter proposed in #1009 by @hurry060215-tech (credited as co-author; same public name `ov.single.mrvi`).

- `ov.vi.MRVI`: port of scvi-tools 1.5.2's torch MRVAE (u/z hierarchy, sample-conditioned attention encoder/decoder, mixture-of-Gaussians prior). Downstream: `get_local_sample_representation`, `get_local_sample_distances`, `get_aggregated_posterior`, `differential_abundance`, `differential_expression`, save/load.
- Architecture parity: with copied weights, inference/generative outputs are bit-identical to scvi-tools.
- Validation (Wilk 2020 COVID PBMC, 13 donors, 12k cells, 2000 HVG, 3 seeds, H100): ELBO within 0.3%; ARI/NMI/ASW match; ours-vs-ref correlations are at or above the reference's own seed-to-seed agreement (sample distances r 0.921 vs ref-ref 0.894; DE mean log2FC r 0.966 vs 0.960; DA r 0.90–0.93). 1.0–1.5× faster.
- AnnDataOOM and Dask on the real cohort: ELBO within 0.03% of in-memory, sample-distance r > 0.93.
- `cuda_graph` defaults to False for MRVI (capture fails for its reparameterisation).
- Not ported: outlier cell-sample pairs, admissibility-filtered DE, lfc_std/pde.
- tests/vi on merged tree: 60 passed, 2 skipped. Details: `benchmarks/vi/results_mrvi.md`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6b73995ba81`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.