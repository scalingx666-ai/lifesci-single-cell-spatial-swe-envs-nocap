# Issue

**Title:** fix(pp): guard against pyscdblfinder <0.2.0 large-dataset stall

## Description

## Summary

 — two users report `ov.pp.qc(..., doublets_method="scdblfinder")` **stalling overnight with near-zero CPU** on ~100k-cell datasets, while `scrublet` runs fine and running `scrublet` first "unblocks" it.

### Root cause

The reporters are on **pyscdblfinder ≤ 0.1.0**, whose kNN doublet-feature step builds a **full N×N distance matrix** — ~`N²·8` bytes, ≈ **125 GB at 100k cells**. That doesn't fit in RAM, so the process thrashes swap: near-zero CPU, never finishing. (The "scrublet first" workaround isn't scrublet-specific — running `qc` twice means the second call operates on the already-filtered, smaller matrix.)

pyscdblfinder **0.2.0** replaced that with the `O(N·k)` chunked-kNN path and is already on PyPI. But omicverse had **no version floor** on pyscdblfinder — and since `scdblfinder` is the default `doublets_method` and is *lazily* imported, users on the old wheel silently hit the stall.

## Fix

`_resolve_doublets_method` now checks the installed pyscdblfinder **distribution version** and, if it's `< 0.2.0`:
- prints a warning referencing the stall (#848) + an upgrade hint,
- falls back to `scrublet` so the pipeline **finishes** instead of hanging.

Install/upgrade hints now pin `>=0.2.0`.

### Why distribution metadata, not `__version__`

pyscdblfinder 0.2.0 ships a **stale `__version__ = '0.1.0'`** in its `__init__` (the dist metadata is correctly `0.2.0`). So the guard reads the version via `importlib.metadata.version("pyscdblfinder")`, which is trustworthy, rather than the module attribute.

## Tests

`tests/pp/test_scdblfinder_version_guard.py` (**6 passed** locally):
- `0.1.0` installed → falls back to `scrublet`, message cites #848 + `0.2.0`
- `0.2.0` / `0.3.1` → passes through as `scdblfinder`
- package missing → falls back
- other methods unchanged
- `_version_lt` boundary cases

Thanks to @fangzt98 and @BubbleFrog00 for the reports.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `43a0476ac962`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.