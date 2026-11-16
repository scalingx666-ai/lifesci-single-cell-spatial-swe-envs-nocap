# Issue

**Title:** deprecate(rtk): deprecate RealTimeKernel.from_wot (removed in v3)

## Description

## Motivation

Part of slimming the package for CellRank 3.0. `RealTimeKernel.from_wot` is a good candidate to deprecate:

- **Waddington-OT is unmaintained** — no Python 3.14 wheel, and its `POT` dependency needs a fragile from-source C++ build.
- **The path is untested in CI** — `test_from_wot` is `pytest.importorskip("wot")`, so it skips on every CI run; that surface area is effectively unverified.
- **There is a clear, maintained replacement** — `from_moscot` is the actively-developed OT entry point and the one the tutorials/docs use. `from_wot` is not referenced anywhere under `docs/`.
- **No functionality is lost** — `from_wot`'s body has no runtime dependency on `wot` (it just `sc.read`s the per-timepoint coupling `.h5ad` files). Users with pre-computed WOT couplings can keep using them by building the `couplings` dict manually and passing it to `RealTimeKernel(..., couplings=...)`.

This matches the existing v3 deprecation batch (`CFLARE`, `GPCCA.fit`/`predict`, `BaseEstimator.fit`/`predict`, non-deterministic `VelocityKernel` models), all of which use `warnings.warn(..., DeprecationWarning, stacklevel=2)` plus a `.. deprecated::` docstring block.

## Changes

- `from_wot` now emits a `DeprecationWarning` pointing to `from_moscot`, with a `.. deprecated:: 2.2` docstring note describing the manual-couplings migration path.
- `test_from_wot` wraps the call in `pytest.warns(DeprecationWarning, ...)`.

## Testing

Ran the full `from_wot` test end-to-end (with `wot` installed locally), not skipped:

```
uv run pytest tests/test_kernels.py::TestRealTimeKernel::test_from_wot
# 1 passed
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57e84563952b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.