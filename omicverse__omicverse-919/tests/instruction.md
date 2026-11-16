# Issue

**Title:** feat(pl): clinical statistics and publication figure assembly

## Description

`ov.pl` can draw an embedding but could not draw a survival curve. This adds the plots a clinical or benchmarking result actually needs, plus the plumbing to get them out of matplotlib at the size and in the format a journal asks for.

All of it is **data-first**: a `DataFrame` + column names, bare arrays, or an `AnnData` (its `.obs`) are interchangeable. Nothing here requires an `AnnData`.

## What's new

| Function | Draws |
| --- | --- |
| `ov.pl.survival` | Kaplan-Meier + log-log band + censoring ticks + numbers at risk + log-rank + hazard ratio |
| `ov.pl.cumulative_incidence` | Aalen-Johansen under competing risks + Gray's test, with an opt-in `1 - KM` overlay so the naive estimator's bias is visible |
| `ov.pl.roc` | ROC with DeLong intervals, multi-model overlay, one-vs-rest multiclass + macro/micro |
| `ov.pl.confusion` | Confusion matrix + accuracy / balanced accuracy / kappa / per-class P-R-F1 |
| `ov.pl.forest` | Effect sizes with CIs, subgroups, fixed or DerSimonian-Laird random-effects pooling |
| `ov.pl.figure` | Canvas in mm / cm / in / px, or by journal column preset (`'nature-single'` = 89 mm) |
| `ov.pl.multipanel` | Labelled panel grid or mosaic |
| `ov.pl.add_panel_label` | a/b/c tags offset in **points**, not axes fractions |
| `ov.pl.savefig` | Several formats per call, text stays text |
| `ov.pl.set_editable_text` | `svg.fonttype='none'` + `pdf/ps.fonttype=42` globally |
| `ov.pl.take_legend_out` | Legend outside the axes |

The estimators are public on their own too — `kaplan_meier`, `logrank_test`, `aalen_johansen`, `grays_test`, `roc_auc_ci`, `meta_analysis` — and return plain dicts.

**No new dependencies.** The survival estimators are implemented on NumPy/SciPy rather than pulling in `lifelines`.

## Numerical parity

Pinned in `tests/pl/test_stats_layout.py`. The reference packages are **not** needed to run the tests — the expected values are baked in as constants.

| Quantity | Reference | Agreement |
| --- | --- | --- |
| KM survival, log-log band, median + Brookmeyer-Crowley CI | lifelines 0.30.0 | ~1e-12 |
| Multivariate log-rank chi-square | lifelines 0.30.0 | ~1e-10 |
| Aalen-Johansen CIF **and its variance** | lifelines 0.30.0 | ~1e-10 |
| DeLong AUC interval | R pROC 1.18 | 1e-11 |
| Fixed/random pooling, tau², Q, I² | `statsmodels.stats.meta_analysis` | ~1e-12 (checked live) |
| Gray's test | R cmprsk 2.2-12 | **within 2.3%**, see below |

Gray's test uses the subdistribution risk set with the log-rank variance rather than Gray's full martingale variance. Across four simulated cohorts (8 cause/cohort comparisons) the chi-square never differed from `cmprsk::cuminc` by more than 2.3%. That limit is documented in the docstring and asserted at 5% in the test, rather than being papered over.

## Two defects found by running it on real data

Both are regression-tested. Found while building the tutorial against the TCGA Pan-Cancer Clinical Data Resource:

1. **Reference group came from `pd.unique`** — i.e. whichever patient happened to be first in the file. A per-cancer-type forest plot came out with half its hazard ratios inverted (KIRC 0.28, BLCA 2.19, for the same comparison). Level order is now the `Categorical` category order, else sorted, and `groups=` sets it explicitly.
2. **`roc` picked `pos_label` by order of appearance** while `roc_auc_ci` used the sorted classes, so the same model scored AUC 0.79 in one call and 0.21 in another. Both now follow scikit-learn's rule.

## Testing

`tests/pl/test_stats_layout.py` — 73 tests, all passing. Covers the parity table above, the two regressions, input-form equivalence (DataFrame / arrays / AnnData give identical statistics), error messages, and the export contract (an SVG saved with the defaults really does still contain `<text>` nodes; with `editable_text=False` it does not).

## Tutorial

omicverse/omicverse-tutorials#97 — executed end to end on real TCGA data.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01VVqVNig3oV6wz42YiQ9obZ

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51f9f979a9a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.