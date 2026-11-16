# Issue

**Title:** feat(pl): add UpSet plot support

## Description

## Problem

Venn plots are useful for small numbers of sets, but they become hard to read once users compare more than four gene sets or cell-state sets.

## What this adds

Adds `ov.pl.upset` for visualizing exclusive intersections across many sets.

### `ov.pl.upset`

Supports:
- dictionary input: `{set_name: iterable_of_items}`
- AnnData input using boolean columns in `adata.obs` or `adata.var`
- selective row/column coloring through `intersection_color`, `set_size_color`, and `matrix_color`
- OmicVerse style integration through `style=ov.style`
- layout controls including `height_ratios`, bar widths, dot sizes, line widths, grid styling, count labels, and manual row/column ordering
- `max_sets` guard to avoid accidental exponential blowups when too many boolean columns are inferred

Intersection color/order keys are order-insensitive, so `"A&B"` and `"B&A"` refer to the same intersection.

## Notes

- No new dependency is introduced.
- Existing `ov.pl.venn` behavior is unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `359734444d89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.