# Issue

**Title:** CI: faster coverage upload, bump actions; cache numba compilation

## Description

Two small changes to cut CI time and per-session overhead.

### CI
- `codecov/codecov-action` v1 → v7. v1 is deprecated, and its upload step took about 28s of the roughly 2m45 job. The `files` and `token` inputs are unchanged in v7.
- `actions/checkout` v2 → v7 in all workflows. v2 runs on a deprecated Node runtime.

### `cache=True` on scFates' `@njit` functions
`process_R_cpu`, `norm_R_cpu`, `get_SE` and `cdist_numba` are now cached on disk instead of being recompiled in every Python session. Measured locally, the first calls of all four drop from 0.73s to 0.12s in a new session.

This does **not** speed up CI. The test suite runs in a single process, so each function compiles once either way, and CI starts with an empty cache. Most of CI's compile time comes from dependencies (umap, pynndescent), which already cache. Recovering that would mean persisting caches between runs, which needs a committed `pixi.lock`; that's not in this PR.

### Testing
`pixi run test` passes locally. The effect on upload time will show in this PR's CI run.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `58084cae2b69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.