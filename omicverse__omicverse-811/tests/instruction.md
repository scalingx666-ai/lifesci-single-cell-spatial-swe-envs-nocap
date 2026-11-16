# Issue

**Title:** ci: fix py3.11/3.12 build — run on numpy>=2, pin jax<0.7

## Description

. The `py310|py311|py312` build has been failing on 3.11/3.12 (pre-existing on master): the resolver pulls `jax 0.10.x` transitively (via `mellon`), which is broken against numpy 2.4.x — it calls `np.dtypes.StringDType` at import and crashes test collection of `tests/micro/test_*.py`. py3.10 passed because it resolved `jax 0.6.2` with numpy 2.2.6.

omicverse core already supports numpy≥2 (the only `<2.0.0` cap was a stale leftover in the `easy` extra). Fix:
- anchor `numpy>=2` in the CI install (CI now runs on numpy≥2, matching core)
- pin `jax/jaxlib<0.7` → 0.6.2, the version py3.10 proved works on numpy≥2
- drop the stale `numpy<2.0.0` cap in the `easy` extra (now `numpy>=1.23`, == core)

Verified resolution: `numpy>=2` + `jax<0.7` → jax 0.6.2 + numpy 2.4.6, clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e5c6611ad7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.