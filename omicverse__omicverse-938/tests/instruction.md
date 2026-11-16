# Issue

**Title:** feat(pl): place a marsilea heatmap in a region with rect=

## Description

## The problem

marsilea owns its own layout. `freeze` derives a figure size from the block's content, calls `figure.set_size_inches` with it, then adds every axes at `inches / that size`.

Hand it a host figure and it **resizes the host and spreads the heatmap over the whole canvas**. A multi-panel figure could not give the heatmap a corner, so the only way to place one was to render it to a raster and `imshow` the result — losing vector text and every bit of marsilea's own styling (dendrograms, annotation strips, labels, colour bar, legends) as editable output.

## What this adds

`rect=(x0, y0, w, h)` in host-figure fractions:

```python
fig = plt.figure(figsize=(13, 7))
fig.add_axes([0.05, 0.6, 0.3, 0.33])          # some other panel
ov.pl.heatmap(adata, figure=fig, rect=(0.06, 0.05, 0.88, 0.48),
              row_annotation="Ensemble", col_annotation="cluster",
              row_dendrogram=True, show_rownames=True,
              xlabel="Genes", ylabel="Patients", label="Z-score")
```

## Why it works this way

- **Rescaling the axes rectangles afterwards is not viable.** A rectangle scales but the text inside it does not, so a block squeezed to half width keeps full-size tick labels and legends, which then overflow. Only a *translation* is safe.
- **So the size is arranged before the draw.** The overhead around the heatmap cell — dendrograms, annotation strips, labels, legends, margins — is set in inches and does not depend on how large the cell is, so one throwaway render measures it: `overhead = natural_figure_size − trial_cell_size`. The cell that makes the block exactly fill `rect` is `rect_size − overhead`.
- The block is built at that cell size and **translated** into place; the host's figure size is restored. Nothing is scaled, so labels, colour bar and legends keep the size they were drawn at.

`width` / `height` are exposed too, for sizing the heatmap cell directly.

## Also

Corrects the `_render_into` docstring, which claimed the rectangles marsilea computes "are already fractions of the target region". They are fractions of the size marsilea derived — which is why a SubFigure target was never actually confined; the no-op `set_size_inches` only stops the call from raising.

## Tests

`tests/pl/test_marsilea_heatmap.py` — the host figure keeps its size, every axes stays inside the region, a panel already on the figure is untouched, a wider region gives a wider block (the cell is resized, the block is not shrunk inside), and `rect` without `figure` is refused.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `174dd04cc526`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.