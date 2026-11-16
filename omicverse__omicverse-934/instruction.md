# Issue

**Title:** feat(pl): an embeddable clustered heatmap on marsilea

## Description

`ov.pl.complexheatmap` (PyComplexHeatmap) builds its own figure, so it can't be one panel of a larger figure. `ov.pl.heatmap` is a **marsilea**-backed alternative that renders into a caller-supplied Figure or **SubFigure** — which is what makes it embeddable.

```python
fig = plt.figure(); left, right = fig.subfigures(1, 2)
ov.pl.heatmap(adata, figure=left, row_annotation='celltype')
# every axis lands inside `left`; `right` is untouched
```

Accepts an array, a DataFrame or an AnnData (annotations pulled from `.obs`/`.var` by name); z-score by row or column; row/col clustering with dendrograms; categorical annotations get discrete colours, numeric a gradient. Returns the marsilea Heatmap with `.row_order`/`.col_order` attached.

**No PyComplexHeatmap anywhere** (only a docstring line contrasting it).

Two places the marsilea 0.5.8 API does not behave as its signature suggests, handled and documented:
- `render(figure=SubFigure)` raises once a dendrogram or annotation is added — the composite layout's `freeze()` calls `figure.set_size_inches` unconditionally, and `SubFigure` has none (its size belongs to the parent gridspec). Worked around by attaching a no-op `set_size_inches` to the SubFigure for the duration of `render`; marsilea's rects are already `[0,1]` fractions, so the region fills correctly.
- `row_cluster`/`col_cluster` are read-only bool properties, not methods; clustering is driven by `add_dendrogram(show=...)`, so a dendrogram is honoured only when its axis is clustered.

7 tests, structure not pixels: SubFigure isolation (axes' `.figure` is the sub, sibling empty; red evidence that rendering into the parent fails it), standalone figure, AnnData annotation from `.obs`, `z_score=0` centres rows, clustering reorders, length-mismatch annotation raises.

Guarded import: an actionable ImportError if marsilea is absent, so this adds no hard dependency.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9cac8651a29d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.