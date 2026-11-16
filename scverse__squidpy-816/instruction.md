# Issue

**Title:** More robust co-occurrence calculation

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description

 I modified `_occur_count`  in gr/_ppatterns.py to enable more robust calculation of the co-occurrence probability ratio. My changes include:

1) Modified intervals from discrete interval bins to increasing radii sizes.

`idx_x, idx_y = np.nonzero((pw_dist <= thres_max) & (pw_dist > 0))`

instead of

`idx_x, idx_y = np.nonzero((pw_dist <= thres_max) & (pw_dist > thres_min))`

This enables retainment of more cells within a given distance threshold, which is especially important when certain cell types are very scarce. Visually, the co-occurrence plots are smoother and less jagged.

2) Modified the way co-occurrence pairs are counted (lines 297-301).

`np.triu_indices_from` called in the `co_occurrence` function returns the indices of non-repetitive pairs of splits, meaning the pair (split i, split j) only occurs once. If cell A from split i and cell B from split j are proximal (i != j), then both need to be counted, i.e. conditioned on A, B is proximal, and conditioned on B, A is also proximal.

3) Modified the way conditional probability is computed (lines 303-316).

When certain cell types are scarce or not within a given distance threshold, division by zero errors may occur. Special handling needs to be done to ensure that the co-occurrence values are not nans and can be plotted.

## How has this been tested?

This has been tested on the Xenium breast cancer tumor microenvironment Dataset in the 'Analyze Xenium data' tutorial, as well as on a toy dataset. The code has passed all local tests as indicated by the Contributing guide.

### Tutorial dataset

Before modifications:
<img width="703" alt="Screen Shot 2024-04-16 at 5 07 11 PM" src="https://github.com/scverse/squidpy/assets/76278056/da64abe3-dde9-40cc-826a-9c229974696d">

After modifications:
<img width="701" alt="Screen Shot 2024-04-16 at 5 07 01 PM" src="https://github.com/scverse/squidpy/assets/76278056/b23c46c1-90d4-4e2e-b389-646d29b7d69b">

Notice that the plot is smoother and less jagged.

### Toy dataset

Spatial plot:
<img width="649" alt="Screen Shot 2024-04-16 at 5 22 52 PM" src="https://github.com/scverse/squidpy/assets/76278056/bf312a92-3e0a-40e7-b01a-9ea2f11d9796">

Before modifications:
<img width="710" alt="Screen Shot 2024-04-16 at 5 23 00 PM" src="https://github.com/scverse/squidpy/assets/76278056/a353e4b5-f5fd-4ba4-8b8d-2a653bdd490f">

After modifications:
<img width="708" alt="Screen Shot 2024-04-16 at 5 23 09 PM" src="https://github.com/scverse/squidpy/assets/76278056/68f5ab9b-1eb4-4cd4-a5ca-d57c145da41a">

The parameters `interval=np.arange(0, 2000, 100), n_splits=2` are used to compute co-occurrence. Without handling of division by zero errors, the values beyond 400 for cells of type 1 and type 3 as well as all values for cells of type 2 become nans and cannot be plotted accurately, whereas a robust handling of division by zero errors yields a calculation that is a better representation of the actual co-occurrence relationship.

## Closes

<!-- If applicable, type `closes #XXXX` in your comment to auto-close the issue that this PR fixes. -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb43d6221582`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.