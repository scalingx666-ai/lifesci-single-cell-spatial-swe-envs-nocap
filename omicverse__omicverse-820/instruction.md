# Issue

**Title:** feat: global random seed for reproducibility — ov.set_seed

## Description

.

## Problem

Randomised steps (UMAP, leiden, neighbors, doublet detection, the GPU/torch backends) could give different results across runs. There was no single place to fix reproducibility.

## What this adds

`ov.set_seed(seed=0, deterministic=False)` — seeds **every RNG backend omicverse touches in one call**:
- Python `random` + `PYTHONHASHSEED`
- NumPy
- PyTorch (CPU + all CUDA devices)
- MLX (Apple, if installed)

and records it in `ov.settings.seed`. Also available as `ov.settings.set_seed(...)`.

```python
import omicverse as ov
ov.set_seed(0)   # at the top of your script/notebook
# ov.pp.neighbors / ov.pp.umap / ov.pp.leiden ... now reproducible
```

`deterministic=True` additionally requests deterministic GPU kernels (`cudnn.deterministic=True`, `cudnn.benchmark=False`, `torch.use_deterministic_algorithms(True, warn_only=True)`, `CUBLAS_WORKSPACE_CONFIG`) for bit-level reproducibility, trading some speed.

Functions that already expose `random_state`/`seed` keep honouring an explicit value; `set_seed` fixes the **global** generators they fall back on plus the non-seedable corners of the GPU paths.

## Tests

`tests/test_set_seed.py` — top-level + settings exposure, `settings.seed` recording, and reproducibility of NumPy / Python `random` / torch, plus the `deterministic=True` path. All pass.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e4d86acfe47`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.