# Issue

**Title:** fix(pp/ambient): envelope refuses a raw matrix it cannot align with the cells

## Description

## Problem

`method='envelope'` (#996) defines empty droplets as *raw barcodes that are not called cells* (`_empties_from_raw`). Two inputs used to fail silently:

1. **Barcodes don't overlap.** Suppose `raw.obs_names` does not contain the called cells, for example a simulated `raw` built with names `c0…`/`e0…` while the cells keep their real barcodes. Then **every** raw row, cells included, was treated as an empty droplet, and the soup profile became the cells' own expression profile. No error, no warning.
2. **Genes are in a different order.** `raw.X[mask]` was taken positionally, so a `raw` whose genes were ordered differently mixed genes.

We found this in an omicos agent run. The agent benchmarked `envelope` on its own simulator using mismatched barcodes. It got gap −0.26, worse than no correction, and abandoned the method, even though the same method passes the real task. The bug sat in the input wiring, not in the method itself.

## Fix

- None of the called cells appear in `raw.obs_names` → `ValueError` that shows example barcodes from both objects.
- Some called cells are missing from `raw` → `UserWarning`.
- `raw` genes are reindexed to `adata.var_names`. If any genes are missing → `ValueError`.

## Tests

New file `tests/pp/ambient/test_envelope_raw_alignment.py` with 5 tests: matching raw, disjoint barcodes, partial overlap, shuffled gene order, missing genes. `tests/pp/ambient` passes locally: 10 passed.

Correct inputs give unchanged results. The new checks only fire on inputs that were already silently wrong.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d60d0f8418e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.