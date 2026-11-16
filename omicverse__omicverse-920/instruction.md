# Issue

**Title:** feat(pl): table-first statistical plots and an AnnData adapter

## Description

Second cut of the `ov.pl` work. **Stacked on #919** — base is `feat/pl-stats-layout` so the diff shows only this change; retarget to `master` once #919 merges.

Almost every plot in `ov.pl` starts from an `AnnData`. That is right for an embedding; it is in the way for the ordinary figures a paper is made of — a bar chart with a test on it, a histogram, a ridgeline, a regression, a Q-Q plot. Those need a column of numbers and a column of labels.

## Fifteen table-first plots

`barplot` `stripplot` `violinplot` `stackplot` `pieplot` `donutplot` `lollipopplot` `slopeplot` `histplot` `kdeplot` `ridgeplot` `qqplot` `scatterplot` `lineplot` `regplot`

Each takes a `DataFrame` + column names, bare arrays, or an `AnnData` (its `.obs`) — interchangeably.

The `...plot` suffix keeps this layer clear of the omics-specific names. **`ov.pl.violin` still takes an `AnnData`** and knows about genes and layers; `ov.pl.violinplot` takes a frame. No existing function changes behaviour.

## Statistics that match the picture

`ov.pl.compare_groups` runs the comparison and returns a tidy table — automatic test selection (Mann-Whitney pairwise + Kruskal-Wallis omnibus by default, ANOVA when the pairwise test is parametric), explicit `pairs=`, Holm / Bonferroni / BH correction. `ov.pl.add_stat_annotation` draws the brackets **from that table**, stacking them so they never overlap and extending the axis to fit.

Every categorical plot takes `test=` and routes through the same code, so the stars on the figure and the numbers in the text cannot drift apart. `ov.pl.add_palue` still exists for hand-placed annotation; this is the version that runs the test.

## Not tied to AnnData

- **`ov.pl.as_plotdata(data)`** — one accessor, `values(key)`, resolving a name against metadata first and features second. Dense or sparse, `AnnData` / `DataFrame` / `dict` / array+`obs`.
- **`resolve_columns` now goes through it**, so a gene name works anywhere a column name does: `ov.pl.violinplot(adata, 'louvain', 'CD3D')` needs no manual extraction.
- **`@ov.pl.accepts_frame`** — the retrofit path for existing `AnnData`-shaped plots. Wraps a `DataFrame` in `ObsView`, a metadata-only view. Deliberately *not* a fake `AnnData`: reaching for `.X` raises immediately naming the problem, instead of failing later on an empty array. String columns become categorical on construction because that is what `anndata` does, and `.obs` is a copy so drawing a plot never mutates the caller's frame.
- `cellproportion` and `cellstackarea` are converted as proof; the tutorial shows how to apply it to your own function.

## Validation

`tests/pl/test_generic_plots.py` — **93 tests**. Every computed quantity is checked against a reference on the same data, not just "the plot ran":

| Quantity | Checked against |
| --- | --- |
| Pairwise + omnibus P values | `scipy.stats` (mannwhitneyu, ttest_ind, brunnermunzel, kruskal) |
| Holm correction | `statsmodels.multipletests` |
| Bar heights, SE error bars | `numpy` / `pandas` |
| Histogram counts, density, probability, fill | `numpy.histogram` |
| KDE curve | integrates to 1 |
| Ridge ordering and medians | `pandas.groupby` |
| Regression slope / intercept / R² | `np.polyfit`, `scipy.linregress` |
| Paired slope test | `scipy.wilcoxon` |
| λ<sub>GC</sub> | ≈ 1.0 on uniform P values; > 1.2 when inflation is real |

Also asserted: the three input forms give identical numbers, the generic names do not shadow the omics ones, and every error message names the problem.

## Two defects found by drawing real figures

- `lollipopplot` returned its table with internal column names (`x`/`y`) rather than `label`/`value`.
- A pie of ten PBMC populations, three of them under 2%, was unreadable — hence `other_threshold=` (which prints exactly what it merged) and `legend=True`.

## Testing

93 new tests pass; the whole `tests/pl` suite is **424 passed**.

## Tutorial

omicverse/omicverse-tutorials#98 — executed end to end on `pbmc68k_reduced`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01VVqVNig3oV6wz42YiQ9obZ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5317bf907528`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.