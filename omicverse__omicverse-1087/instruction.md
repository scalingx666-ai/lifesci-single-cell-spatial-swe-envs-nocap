# Issue

**Title:** ov.vi.SysVI: native SysVI (replaces #1013, no scvi-tools)

## Description

Native PyTorch SysVI on ov.vi, replacing the scvi-tools adapter proposed in #1013 by @hurry060215-tech (credited as co-author; same public name `ov.single.sysvi`), plus `ov.single.batch_correction(methods='sysVI')` → `obsm['X_sysVI']`.

- `ov.vi.SysVI`: Gaussian cVAE on normalised expression, `VampPrior` (new in `_priors.py`), latent cycle-consistency loss, system + categorical/continuous covariates.
- Parity: with copied weights (dropout off) reconstruction/KL/cycle losses are bit-exact vs scvi.external.SysVI; VampPrior matches to ~2e-7.
- Validation (Baron 2016 pancreas, human vs mouse, GSE84133, 10,455 cells, 2000 HVG, 3 seeds, 400 epochs, H100): iLISI 0.130±0.04 vs 0.105±0.01; kBET 0.666 vs 0.629; NMI 0.897 vs 0.898; ARI 0.928 vs 0.931 — all within seed spread; ~4.8× faster. AnnDataOOM and Dask reproduce the in-memory latent exactly.
- Core fix: `_categories()` now uses content-sorted categories (OOM/Dask readers could reconstruct a categorical's category order differently than pandas, silently swapping batch codes between backends), keeping the native dtype of integer categories.
- `cuda_graph` defaults to False for SysVI (capture fails with decoder dropout).
- tests/vi + batch tests on merged tree: 85 passed, 3 skipped. Details: `benchmarks/vi/results_sysvi.md`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4764fedb247c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.