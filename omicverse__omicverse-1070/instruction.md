# Issue

**Title:** Fix CI after the scanpy decoupling; require anndataoom-fast>=0.1.6

## Description

Fixes the 7 failures #1069 left on py3.10/3.11/3.12:
- 4 × `TypeError: leiden_gpu_sparse_multilevel() got an unexpected keyword argument 'flavor'` (space niche / STAGATE / SpaceFlow): `ov.pp.leiden` now runs the CPU Leiden when CPU-only arguments (flavor / n_iterations / directed) are given in mixed / gpu mode; `_sc_compat` neighbors / leiden / umap always use the CPU path like the scanpy calls they replace.
- 3 × gsmap tests patched scanpy's normalize_total / log1p; they now patch `ov.pp`.
- New regression test `tests/pp/test_leiden_mode_fallback.py` (fails on the old code, passes now).
- `anndataoom-fast>=0.1.6` (released): UMAP no longer stalls on small graphs with many OpenMP threads.

Local: the 7 previously failing tests + the new test pass (STAGATE / SpaceFlow runtime tests need torch, not installed locally).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63de61011e7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.