# Issue

**Title:** fix(pl): upset takes a host figure; dotplot's legend side is a choice

## Description

Two changes, and one thing I got wrong and reverted.

## `upset` can be a panel

It built its own figure with `plt.figure` and returned it, so it could not go into a composition. It is four plain matplotlib axes in a 2×2 gridspec, so `figure=` plus `rect=(x0, y0, w, h)` is enough — the gridspec is confined with `left/right/bottom/top` and the host keeps its size.

```python
fig = plt.figure(figsize=(12, 6))
ov.pl.upset(sets, figure=fig, rect=(0.45, 0.08, 0.50, 0.42))
```

Standalone behaviour unchanged: no `figure`, new figure sized by `figsize`, still returns `(fig, axes)`.

## `dotplot` legends are no longer stuck on the right

It hardcoded `m.add_legends(box_padding=2)`, so the dot-size key and the colour bar always stacked into a column beside the dots — which is also what makes the block too wide for a narrow panel. Now: `legend_side` (`'right'`/`'left'`/`'top'`/`'bottom'`), `legend_pad`, and `legend=False`.

## What I reverted, and why

I first gave `dotplot` `figure=`/`rect=` too, assuming the marsilea block could be rendered at its natural size and translated, the way  does for `ov.pl.heatmap`. **It cannot.**

marsilea's layout for a `SizedHeatmap`-plus-legends block is *composite*, and `freeze` only calls `set_size_inches` for **non**-composite layouts. So the block never reports a size: its axes are fractions of whatever figure it is handed, and it fills that figure however large it is. Measured — the same 4-gene block spans **650 mm across in a 30 inch figure**, and does so at font size 7, 9 and 12 alike.

Translation cannot confine something that scales with its container, and rescaling would shrink the axes without shrinking the tick labels, the dot-size key or the colour bar. Placing such a block properly needs marsilea's own layout anchors (`set_figsize` / `set_anchor`), which is a larger change than this PR.

So `dotplot` keeps building its own figure, and the reason is now a comment in the source rather than an argument that silently does the wrong thing.

## Tests

`tests/pl/test_panel_embedding.py` — upset: host size survives, an existing axes is untouched, new axes stay inside the region, standalone unchanged, `rect` without `figure` refused. dotplot: every legend side works, legends can be switched off, an unknown side is refused.

Full `tests/pl/`: 706 passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e6b68411bb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.