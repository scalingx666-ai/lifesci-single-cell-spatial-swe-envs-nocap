# Issue

**Title:** fix: repair Read the Docs build broken by legendkit 0.4.1

## Description

## Problem

The Read the Docs build fails. `docs/examples/Basics/plot_stacked_bar.py` cannot execute, so sphinx exits 2:

```
ValueError: colors and labels must have the same length, got 16 colors and 5 labels
  File "src/marsilea/plotter/bar.py", line 404, in get_legends
  File "legendkit/_legend.py", line 469, in __init__
```

This is a library bug, not a docs bug. `StackBar` falls back to the 16-color `ECHARTS16` palette regardless of item count. `render_ax` already trimmed the palette to the data (`self.bar_colors[: len(data)]`), but `get_legends` passed all 16 colors alongside the real labels. The mismatch was harmless until legendkit 0.4.1 added length validation, which this repo picked up in #91.

Any `StackBar` with a legend and fewer than 16 items is affected, not just the docs.

## Changes

- `src/marsilea/plotter/bar.py` — trim the legend colors to the labels, matching what `render_ax` already does.
- `tests/test_plotters_smoke.py` — the existing `test_stackbar` never called `add_legends()`, so it could not catch this. Added a case that does.
- `readthedocs.yaml` — RTD checks out a shallow clone with no tags, so `uv-dynamic-versioning` could not derive a version and fell back to `0.0.0`. Since `conf.py` sets `release = ma.__version__`, the published docs advertised `0.0.0.post1.dev0`. Fetch tags in `post_checkout`.
- `docs/.gitignore` — `how_to/*.png` and `how_to/*.pdf` miss the artifacts sphinx-gallery writes one level deeper (`how_to/save/plot.png`). Widened to `how_to/**/*`.

## Verification

- Clean `sphinx-build` from scratch (`docs/clean_up.py` first): exit 2 before, **exit 0 with zero warnings** after.
- `pytest tests/test_plotters_smoke.py`: 20 passed.
- Version fallback reproduced on a `git clone --depth 1 --no-tags` checkout: `0.0.0.post1.dev0` before the `post_checkout` fetch, `0.6.2.post4.dev0` after.
- Audited the other four `CatLegend` call sites. `_seaborn.py` builds its palette with `dict(zip(hue, colors))` and `mesh.py` uses `cycle()` with `enumerate`, so both self-truncate. `bar.py` was the only one affected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea9a3419482e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.