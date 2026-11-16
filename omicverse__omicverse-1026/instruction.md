# Issue

**Title:** perf(single): 8.6x faster pseudobulk for sample x cell-type cohorts

## Description

## TL;DR

- This PR makes `ov.single.pseudobulk` faster when a cohort has many sample x cell-type profiles.
- It replaces three per-profile Python loops with one-pass NumPy steps and builds string keys once per profile, not per cell.
- Median wall time on a 30k-cell cohort with about 8k profiles: 4.12 s -> 0.48 s, 88% faster (8.6x).
- `pytest tests/single/test_pseudobulk.py -q` passes (8 passed), and the output is identical to the current code.

## What & Why

Before, the function did extra work for each profile. It ran `np.where(inv == p)` once per profile to find the first cell. For each obs column, it compared the cells of each profile in a Python loop. It also built one `f"{sample}\0{group}"` string per cell to make the profile key.

Now the function sorts the cells by profile once. It reuses that order for the first cell of each profile, for the indicator matrix and for the median slices. One vector comparison checks whether an obs column is constant in every profile. The profile key comes from integer codes of the sample and group labels, and each label string is built once per profile. The expressed-cell counts are 0/1 sums, so float32 keeps them exact.

The profile order, the labels, the matrices, the obs columns and their dtypes stay the same.

## Changes

- Sort the cells by profile once and get `first_idx` from that order.
- Build the count indicator matrix once and reuse it for `mode="sum"` and for `psbulk_props`.
- Check constant obs columns with one comparison per column.
- Make the profile key from `pd.factorize` codes, not per-cell strings.
- Count expressed cells in float32.

## Results

Median of 7 calls (50 for the tiny case) on one CPU core. The test data is random sparse counts with 2,000 genes and donor-level obs columns.

| Situation | Before | After | Change |
|---|---|---|---|
| 200 cells, 4 donors x 3 cell types (test-suite size) | 2.26 ms | 2.00 ms | 1.1x faster |
| 30k cells, 40 donors, per sample only | 112 ms | 96 ms | 1.2x faster |
| 30k cells, 400 donors x 20 cell types | 595 ms | 207 ms | 2.9x faster |
| 100k cells, 400 donors x 20 cell types | 1834 ms | 674 ms | 2.7x faster |
| Mixed cohort: 30k-cell sparse cohort, ~8k profiles, plus dense, mean, median and filter calls | 4.12 s | 0.48 s | 8.6x faster |

Small inputs and per-sample runs have few profiles, so they gain little. They do not get slower.

## Why this is safe and easy to maintain

The change is small and stays in one function. It uses plain NumPy and pandas calls and adds no new branch for special input types. The output is the same as before for sum, mean and median modes, with and without `groups_col`. The existing tests in `tests/single/test_pseudobulk.py` cover these paths.

## Validation

- `pytest tests/single/test_pseudobulk.py -q`: 8 passed.
- Every output was compared exactly with the current code (matrices, layers, obs, var, uns, printed messages and errors).
- Timing check:

```python
import time, omicverse as ov
t = time.perf_counter()
ov.single.pseudobulk(adata, sample_col="donor", groups_col="celltype")
print(time.perf_counter() - t)
```

## AI assistance

This PR was prepared with AI assistance from Aiden. Candidates were tracked with Weco Observe.

Weco share link: https://dashboard.weco.ai/share/YVNh_MzZ18SemMaVq4DN5-ObA_TTvG82

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d94cf1da2d71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.