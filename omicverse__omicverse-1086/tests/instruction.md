# Issue

**Title:** ov.vi.Decipher: native Decipher (replaces #1015, no scvi-tools/pyro)

## Description

Native PyTorch Decipher on ov.vi, replacing the scvi-tools adapter proposed in #1015 by @hurry060215-tech (credited as co-author; same public name `ov.single.decipher`).

- `ov.vi.Decipher`: two-level latent (2-D decipher space v, z), priors, encoder/decoder and ELBO rewritten with torch.distributions (no Pyro); `Trajectory`, `rotate_decipher_components`, `compute_decipher_time`, imputed gene patterns.
- Core (`_train.py`): Pyro-equivalent `ClippedAdam` (CUDA-graph capturable), `drop_last` / `clip_norm` config, per-epoch module hook, `cuda_graph_safe` opt-out, and a fix that benefits every ov.vi model: validation passes no longer consume the global RNG (results previously depended on validation frequency).
- Parity: with identical init/input/RNG, loss equals `pyro.infer.Trace_ELBO` to ~1e-8 relative; replaying scvi's exact minibatch order gives the same trajectory quality.
- Validation (NeurIPS 2021 BMMC erythroid lineage, 4,454 cells, Palantir pseudotime as ground truth, 16 seeds each, H100): trajectory |ρ| 0.824±0.082 vs 0.862±0.058 (ref: 1 additional seed diverged); bad-optimum rate 4/16 vs 2/16, Fisher p=0.65, Mann–Whitney p=0.28 — not significant. Held-out ELBO equal within spread; ~14× faster.
- AnnDataOOM and Dask reproduce the in-memory result exactly.
- tests/vi on merged tree: 72 passed, 2 skipped. Details: `benchmarks/vi/results_decipher.md`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af078c66d142`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.