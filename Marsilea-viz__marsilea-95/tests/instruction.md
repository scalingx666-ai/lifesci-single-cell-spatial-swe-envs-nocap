# Issue

**Title:** fix: pin categorical axis of seaborn plotters so they stay aligned

## Description

## Problem

Seaborn-backed plotters (`Bar`, `Box`, `Boxen`, `Violin`, `Point`, `Strip`, `Swarm`) could drift out of alignment with the rest of a cross-layout.

`_SeabornBase.render_ax` never pinned the categorical axis — it handed the limits entirely to seaborn's `_adjust_cat_axis`, which has two problems:

1. It infers the category count from `n = len(ax.get_xticks())` — the tick count, not the data — and skips outright when the categorical variable isn't string-typed (`native_scale=True`).
2. It sets the limits with `ax.set_xlim(..., auto=None)`, which **leaves matplotlib autoscaling enabled**. The correct limits are only armed, not fixed; the next autoscale request snaps the axis to the artists' extent plus margins.

Because the recomputed extent is the artists' spread, how far the axis moves is data-dependent — which is why strip/swarm with many points was the visible case.

### Reproduction (seaborn 0.13.2 / matplotlib 3.10.0)

Heatmap 12×12 with a seaborn plotter on a flank; the categorical span should be exactly 12:

| Trigger | Result |
|---|---|
| `mp.Strip(data, native_scale=True)` (any plotter) | span 12.10–12.98 — misaligned straight out of `render()` |
| any post-render touch of the plotter's axes (`ax.scatter`, `ax.plot`, `ax.margins`, an overlay, a shared axis) | span 12.10–12.98 — **224/224** configs (7 plotters × 4 sides × split × hue × native_scale) |
| point-count dependence | `Swarm` 12.34 (5 pts) → 12.98 (25+ pts); `Strip` ~12.30; `Bar`/`Box` a flat 12.98 |

Default untriggered usage happened to render correctly, which is why the failure looked intermittent.

## Fix

New `_SeabornBase._align_cat_axis`, called at the end of `render_ax`. It takes the span from the chunk data rather than from seaborn:

- `spec.data` is `(n_observations, n_categories)` in **both** orientations — `Deformation.transform_row` transposes in and back out — so `shape[1]` is the category count for top/bottom/left/right alike, split or not.
- With `hue`, `spec.data` is one array per hue level; every level has the same width.
- Runs per chunk inside `render_ax`, so each split chunk pins to its own width.
- `set_xlim`/`set_ylim` also turn autoscaling off, so a later rescale can't move it.
- The value axis is untouched, so `StatsBase.align_lim` keeps working.
- Flank plots keep seaborn's inverted categorical axis.

Base class only — all seven subclasses are just `_seaborn_plot = "..."`, and every marsilea-native `StatsBase` plotter (`Numbers`, `Area`, `Range`, `StackBar`, …) already pins its own limits.

## Verification

- New parametrised test `test_seaborn_cat_axis_stays_aligned` (7 plotters × 4 sides): **28 fail before the fix, 28 pass after**.
- Full suite: 310 passed, 6 xfailed.
- 224-config sweep comparing category centres against heatmap cell centres in **display** coordinates after an autoscale trigger: worst offset **0.0000 px** (was 224/224 misaligned).
- Bare-axes docs path unchanged: `Swarm(np.random.rand(50, 10)).render(ax)` → `xlim == (-0.5, 9.5)`; same for dict-input hue data and forced `orient="h"`.
- `ruff check` + `ruff format` clean.

Caveat: the local test runs above were done on the previous base (`ea9a341`). The branch was later rebased onto `main` (`546cd7f`, the RTD fix), which also touches `tests/test_plotters_smoke.py`. The rebase applied with no conflicts, but the suite was not re-run locally afterwards — relying on CI for that.

## Notes for reviewers

The test uses `ax.scatter` as its autoscale trigger rather than `ax.autoscale()`. The latter explicitly *re-enables* autoscaling, which no limit fix can — or should — survive.

Out of scope, found while investigating: layering a seaborn plotter on a mesh canvas (`Heatmap.add_layer(mp.Strip(...))`) is offset by half a cell — mesh uses `0..n`, seaborn `-0.5..n-0.5` — and the mesh's value axis gets clobbered. That needs shifting artists rather than limits, so it's left alone here.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `546cd7fdbd5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.