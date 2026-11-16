# Issue

**Title:** fix(io): pass element positionally to anndata write_basic

## Description

## What

`Lineage` serialization fails on current anndata with:

```
TypeError: write_basic() got an unexpected keyword argument 'elem'
```

breaking `tests/test_lineage.py::TestIO::test_anndata_write` on **all stable CI jobs** (this is the primary reason `main` has been red since the 2026-04-15 scheduled run).

## Why

A newer anndata wraps `write_basic` with the `suppress_autoshard_warning` decorator (added for zarr-v3 autosharding). That wrapper's element parameter is named `val`, not `elem`. `inspect.signature` follows `__wrapped__`, so the parameter *appears* to still be `elem`, but at call time the keyword form `write_basic(f, k, elem=elem.X, ...)` no longer matches.

## Fix

Pass the element positionally (`write_basic(f, k, elem.X, ...)`), which works regardless of the wrapper's internal parameter name.

## Validation

`uv run pytest tests/test_lineage.py::TestIO` → 3/3 pass locally.

> Note: this PR only addresses the `write_basic` regression. The remaining stable-CI failures (two `TestClusterTrends` image comparisons) are a separate transparent-background image-comparison issue handled in a follow-up PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `591d7823d893`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.