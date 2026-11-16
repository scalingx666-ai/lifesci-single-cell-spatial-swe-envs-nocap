# Issue

**Title:** ov.pp.ambient: keep counts sparse, pass n_jobs / random_state, require the 0.1.1 ports

## Description

- `remove_ambient`, the FastCAR/scCDC wrappers and `count_integrity_check` no longer densify the count matrix (each copy of a 12k × 33k matrix is ~3.4 GB float64); the per-cell removed fraction and the integrity statistics come from sparse sums. Same outputs.
- `method='decontx'`: `n_jobs` passed to pydecontx (threads; result unchanged).
- `method='sccdc'`: `random_state` passed through, default 1 — R scCDC always fits its curves from `set.seed(1)` (Seurat's `subset` calls `WhichCells(seed = 1)`), so this reproduces R.
- Ambient extras now require pysoupx / pydecontx / pyfastcar / pysccdc ≥ 0.1.1, the releases that reproduce R SoupX 1.6.2, decontX 1.8.0, FastCAR 0.1.0 and scCDC 1.4 (technical reports: omicverse.org/articles/pysoupx, pydecontx; pyfastcar and pysccdc in omicverse-org-home#45/#47).

Tests: `tests/pp/ambient` 28 passed, 3 skipped; end-to-end on 10x hgmm 1k all four methods run with sparse output and pass the integrity check (scCDC: 18 GCGs, as R).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2340a96ee3e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.