# Issue

**Title:** fix(pp): coerce Leiden resolution to a scalar float

## Description

## Problem —
On the `cpu-gpu-mixed` torch Leiden path, a **length-1 list/tuple** `resolution` (e.g. `resolution=[1.0]`, as produced by some agent-generated code) crashed with an opaque error:
```
File ".../pp/_leiden_gpu.py", line 160, in _local_move
    gains = k_ic - resolution * ki * sig_eff / two_m
TypeError: only integer tensors of a single element can be converted to an index
```

**Root cause:** with a *list* `resolution`, `resolution * ki` is Python **list-repetition** (`list.__mul__`), which calls `ki.__index__()` on a multi-element tensor. Reproduced exactly: `[1.0] * torch.arange(5)` → this error (`1.0` / `np.float64(1.0)` are fine).

## Fix
- `leiden_gpu_sparse_multilevel` coerces `resolution` via a new `_coerce_resolution()` at entry — unwraps length-1 `list`/`tuple`, accepts numpy/torch scalars & single-element arrays, and rejects multi-element input with a clear message.
- `ov.pp.leiden` wrapper also normalises a length-1 list/tuple (torch-free) so the `cpu` (scanpy) and `gpu` (RAPIDS) backends are protected too.

## Tests
`tests/pp/test_leiden_resolution.py` — unit-tests the coercion (unwrap + reject), and an integration test running `leiden_gpu_sparse_multilevel(adata, resolution=[1.0])` end-to-end (3/3 pass; previously raised the index TypeError).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4d6e627f92a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.