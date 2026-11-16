# Issue

**Title:** fix: multi-column groupby crashing on non-string observations

## Description

For multi-column `groupby`, `_prepare_dataframe` joins the key values
with `"_".join` over raw values and takes ordering levels from
`.cat.categories`. A non-string key column (integer categorical, plain
numeric) or a NaN row then fails with `TypeError: sequence item 1:
expected str instance`. Single-key `groupby` handles the same columns
correctly. The breakage is specific to the multi-key join. The shared
helper is used by `dotplot`, `matrixplot`, `stacked_violin`,
`tracksplot`, `heatmap` and the dendrogram path, so they all gain the
fix.

- Joined elements pass through `str()` individually.
- Ordering levels come from `.cat.categories` on categorical columns
  and `np.unique` otherwise.
- Rows missing any key value join to no category, matching the
  single-column path where `NaN` never forms one.

#### Tests

`test_plotting.py` gains parametrized `test_multi_groupby_nonstring`
and `test_multi_groupby_partial_nan`. Integer-categorical and numeric
second keys plus partially-NaN keys are pushed through `sc.pl.dotplot`
and `sc.pl.matrixplot`, with joined labels asserted on the returned
plot object. The pre-existing `test_violin` image-compare failures in
this file are seaborn drift, identical on `main`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `50bb2b08b973`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.