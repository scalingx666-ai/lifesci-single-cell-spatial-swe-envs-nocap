# Issue

**Title:** feat: significance annotation for the seaborn plotters

## Description

.

Adds `annotate_stats()` to `Bar`, `Box`, `Violin`, `Strip` and `Swarm`: it runs a statistical test on pairs of categories and draws the result on the plot, using [statannotations](https://github.com/trevismd/statannotations).

```python
box = mp.Box({"Control": control, "Treated": treated}, label="Expression")
box.annotate_stats(pairs="hue", test="Mann-Whitney", text_format="star")

h = ma.Heatmap(treated.values - control.values)
h.group_cols(np.where(up, "Up", "Down"), order=["Up", "Down"])
h.add_top(box, size=2)
h.render()
```

`pairs` takes an explicit list, `"hue"` (levels within each category) or `"all"` (categories against each other); `ref=` narrows either shorthand to one reference, and `pvalues=` annotates values computed elsewhere. Everything after `pairs` is forwarded to `Annotator.configure`, so `test`, `text_format`, `loc` and `comparisons_correction` behave as documented upstream.

All seven wrappers work — `Bar`, `Box`, `Boxen`, `Violin`, `Point`, `Strip`, `Swarm`. statannotations implements neither boxenplot nor pointplot; marsilea does the drawing, so that limit does not apply.

## Division of labour

**statannotations does the statistics**: `StatTest` (the test catalogue), `ComparisonsCorrection` and `PValueFormat`. None of those import seaborn.

**Marsilea draws every bracket**, in figure coordinates, from the options seaborn was actually called with. Its `Annotator` is not used — and with it goes the dependency on `_CategoricalPlotter`, `var_levels`, `iter_data` and `sns._stats.density.KDE`, which was the fragility that made this an optional extra to begin with.

One drawer means within-group and cross-group brackets are identical by construction rather than by matching numbers. They were not: line width 1.5 vs 1.2, stem 2.64px vs 5.40px, black label vs `"0.2"` — and `configure(color=…, line_width=…)` reached only one of them.

## Four things the integration has to get right

- **Labels survive the deform.** Categories are named with the columns of the input, but `data_validator` drops them and the melt is chunk-local positional. Labels are captured in `__init__` and pushed through the *same* `get_deform_func()` as the data, so a bracket stays attached to its category through grouping and clustering. Marsilea owns the label→position mapping and statannotations only ever sees positions, which leaves seaborn's `native_scale` handling untouched.
- **Two-phase render.** Brackets grow the value axis, so annotating inside `render_ax` would undo `align_lim`. `render` now runs render → unify → annotate → unify.
- **Inverted axes.** A left-side plot has its value axis inverted. Brackets and labels are placed from a computed outward direction, so they land past the data either way. Rotated labels need `ha`, not `va` — matplotlib aligns the *rotated* bounding box.
- **Cross-group pairs.** A pair whose members land in different groups is bracketed **across** their Axes. `Annotator` binds to one Axes and cannot do this, so marsilea draws those in figure coordinates — cheap, because after `align_lim` every chunk shares one value scale (a value maps to the same figure position everywhere, so only the categorical ends need each chunk's transform) and `_chunk_names` already says which group a category ended up in. The test still comes from statannotations' `StatTest`, corrections from `ComparisonsCorrection` and the label from `PValueFormat`, configured from the same kwargs, so a spanning bracket cannot disagree with the ones beside it. `ref` reaches across groups too; bare `pairs="all"` deliberately stays inside each group (36 brackets across a 9-category split is not a figure).

Also fixes supplied `pvalues` on a split canvas, which passed the whole list to every chunk regardless of how many pairs that chunk drew. Each chunk now gets its own share, and `pvalues` with a shorthand `pairs` is rejected — there is no stated order for a value to belong to.

## What owning the drawing bought

- **A real bug fixed.** seaborn leaves `stripplot`/`swarmplot`/`pointplot` undodged by default while statannotations *requires* dodge, so brackets pointed at empty space either side of overlaid points. Positions now come from the options seaborn was called with — verified against the drawn artists across 14 combinations of plot type, `width`, `gap`, `dodge` and `native_scale`. A pair whose sides genuinely coincide is refused with a warning naming the fix.
- **Heights come from what was drawn** — whisker caps, error bars, outliers, violin bodies — read from the artists. The violin body is read from its `PolyCollection` vertices, which is exact; statannotations recomputes the KDE because its own `PolyCollection` path is marked "not working".
- **Correction covers every comparison at once.** Per-Axes correction under-corrected a split canvas.
- **Row heights are solved, not guessed.** A label row is a known number of points, so its share of the panel is known and the value range follows from what is left for the data. A layout audit over 12 configurations checks that no label touches a bracket, overlaps another label, or leaves the panel.

## Dependency

`statannotations` is an optional extra, `pip install marsilea[stats]`, imported lazily with a `pip install` hint — modelled on the `fastcluster` handling in `dendrogram.py`. `statsmodels` rides along in the extra because multiple-comparison correction needs it, and `pairs="hue"` generates one test per category.

Only the statistics are imported, and none of that touches seaborn's internals — so a seaborn release can no longer break annotation. `width` / `gap` / `dodge` / `native_scale` are honoured rather than warned about.

## Docs

- Tutorial: `docs/source/tutorial/stats_annotation.rst` — conditions, naming categories, shorthands, grouping/clustering, orientation, precomputed p-values (7 worked figures), linked from the Tutorial index.
- Gallery: `docs/examples/Gallery/plot_stats_annotation.py`.
- The generated seaborn docstrings gain a non-executed snippet for the supported classes, and `Box.annotate_stats` is listed in the API reference.

## Verification

- 553 tests pass (36 new in `tests/test_stats_annotation.py`), `ruff check src` clean.
- Pair resolution is tested as pure logic with no extra installed; the rendering tests `importorskip` statannotations and cover all five plots, all four sides, split canvases, clustered columns, inverted axes and the cross-group skip.
- Docs build with no new warnings; all tutorial and gallery figures render.
- Verified against seaborn 0.13.2 / statannotations 0.7.2 on Python 3.12.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dbba02eae17a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.