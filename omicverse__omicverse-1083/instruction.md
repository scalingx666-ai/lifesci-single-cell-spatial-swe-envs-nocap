# Issue

**Title:** ov.vi.RESOLVI: native ResolVI spatial denoising (replaces #1011, no scvi-tools/pyro)

## Description

Native PyTorch ResolVI on ov.vi, replacing the scvi-tools adapter proposed in #1011 by @hurry060215-tech (with fixes by @mengxu98); both credited as co-authors. Same public name `ov.space.resolvi`, including the protection of spatial inputs from output writes.

- `ov.vi.RESOLVI`: kNN-on-spatial neighbourhood diffusion / background / true-expression mixture rewritten with torch.distributions (no Pyro); semi-supervised `predict()`; `get_proportions`, `get_normalized_expression`, `get_corrected_counts`, save/load.
- Runs on in-memory AnnData, AnnDataOOM and Dask (matching ELBO).
- Core: `make_optimizer` accepts param groups (backwards compatible) for ResolVI's faster-lr per-cell parameters.
- Validation vs scvi.external.RESOLVI 1.5.2 (10x Xenium FFPE breast cancer, 313 genes, 8000 cells, 3 seeds, H100, 40 epochs): marker AUROC 0.941±0.004 vs 0.941±0.003; ARI 0.357±0.010 vs 0.300±0.017; NMI 0.627±0.006 vs 0.598±0.006; ~1.5–4× faster. Bugs fixed on the way: Dirichlet prior sign, KL warmup / Adam eps defaults vs reference. Details: `benchmarks/vi/results_resolvi.md`.
- Not ported: `size_scaling`, differential expression / niche abundance.
- tests/vi on merged tree: 63 passed, 2 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8f5aa8315a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.