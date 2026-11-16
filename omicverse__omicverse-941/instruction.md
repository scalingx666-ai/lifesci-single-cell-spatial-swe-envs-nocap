# Issue

**Title:** fix(pl): qqplot's confidence band was drawn on the theoretical scale

## Description

## The bug

With `dist='norm'`, the x axis is the **standard** normal while y keeps the sample's own units. The band was left in theoretical units:

```
sepal_length:  band  -3.58 .. 3.58
               points 4.30 .. 7.90
```

So it rendered as a detached grey wedge below the data. Found while reproducing the cnsplots showcase Figure 2, where panel **g** is a qqplot — in a multi-panel figure the stray band reads as a second dataset.

## The fix

A pointwise band belongs around the reference line that was actually drawn, so it now travels through the same location-scale map — `slope * ppf(q) + intercept`, with slope/intercept from the quartile fit.

For `line='45'` the map is the identity, and the band staying on the standard scale is the honest reading: the 45° line asserts the sample *is* standard normal, so a band that misses the points is real information, not a rendering error. statsmodels behaves the same way.

Two paths deliberately unchanged, for opposite reasons:

- **`dist='uniform'`** (the GWAS plot) has p values on both axes — its band was already in sample units.
- **non-normal dists** previously drew *no* band at all (`band_lo = ... if dist == "norm" else None`). They now get one from the parameters already fitted to the sample, which is the scale their theoretical quantiles are on.

## Tests

`tests/pl/test_generic_plots.py::TestQqplotConfidenceBand` — the band brackets the sample rather than the origin; a 95% band contains >90% of a normal sample; a fitted gamma gets a band; the uniform/log path is unchanged. Reinstating the old expression fails the first two, so they pin real behaviour.

Full `tests/pl/`: 704 passed.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c3d00678bd8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.