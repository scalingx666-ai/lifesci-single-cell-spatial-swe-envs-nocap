# Issue

**Title:** fix: stop deep-copying live matplotlib artists when composing boards

## Description

## What

Composing an already-rendered board with `/` or `+` crashed on Python 3.14:

```
File "src/marsilea/base.py", line 35, in _copy_board -> new.layout = deepcopy(board.layout)
TypeError: cannot pickle 'itertools.count' object
```

This took down `docs/examples/Gallery/plot_oncoprint.py` at `op /= h`, which made `task doc-build` exit 2 (sphinx_gallery's `summarize_failing_examples`) on any interpreter resolving to 3.14. CI was widened to 3.11–3.14 in dd0ef82, so it is in-matrix.

## Why

`_copy_board` deep-copies `board.layout`. After a render, the layout holds a live `Figure` (`layout.figure`) and the `Axes` of every cell (`cell.ax`). If any axis carries categorical units, that graph reaches matplotlib's `category.UnitData`, which holds an `itertools.count` — and Python 3.14 removed pickle/`__reduce__` support from itertools iterators, so `deepcopy(itertools.count())` now raises where 3.12 returned a copy.

The counter is matplotlib's, not the one in `src/oncoprinter/core.py` — that `count(0, 1)` is consumed by `zip` and never stored.

Object-graph walk from `board.layout` confirms `figure` and `ax` are the only attribute names that ever hold an artist:

```
layout.figure                                  -> Figure
layout.cells['<name>'].ax                      -> Axes
layout.cells['mutation_count'].attach.ax       -> Axes
```

## How

A shared `__deepcopy__` on `BaseCell`, `_MarginMixin` (covers `CrossLayout`, `CompositeCrossLayout`, `StackCrossLayout`) and `_LegendAxes` that nulls `figure`/`ax` instead of copying them.

Dropping them is also semantically right, independent of the Python version: a copied layout is always re-frozen onto its own figure, so the source's figure and axes are stale for the copy. The old behaviour silently built detached duplicate axes and paid to deep-copy an entire figure.

No matplotlib-side workaround (e.g. patching `UnitData.__deepcopy__`) — copying a live figure here was wrong regardless.

## Why the existing tests missed it

`test_composite_*` compose *unrendered* float heatmaps: no live figure, no categorical axis. Two conditions are both needed to reproduce — render before composing, and an axis with categorical units.

The new `test_composite_after_render` adds a `Violin` (seaborn plotters pin a categorical axis), renders both boards, then composes. Verified it fails with the exact `TypeError` when the fix is reverted.

## Verification

- `plot_oncoprint.py` runs clean on 3.14; `uv run --python 3.14 task doc-clean-build` → `build succeeded`
- `520 passed, 6 xfailed` on Python 3.11, 3.12 and 3.14
- New test fails without the fix, passes with it

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd0ef827389d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.