# Issue

**Title:** perf(es): 2.4x faster AUCell CPU scoring (ov.es.aucell benchmark)

## Description

## TL;DR

- This PR makes the CPU kernel of `ov.es.aucell` (`_func_aucell` in `omicverse/es/_aucell.py`) faster.
- It ranks only the top `n_up` genes of each cell inside one parallel numba loop, instead of calling `scipy.stats.rankdata` per cell.
- Benchmark time: 803 ms -> 334 ms, 58% faster (2.4x).
- `pytest tests/test_es_methods.py -k "aucell or test_decoupler_dispatcher" -q` gives 2 passed, the same as on `master`.

## What & Why

Before, `_func_aucell` ran a Python loop over all cells. For each cell it sliced one CSR row, ranked all genes with `scipy.stats.rankdata`, and then called the numba kernel. The kernel only uses ranks up to `n_up`, so most of that ranking work was not used.

Now `_func_aucell` converts blocks of cells to dense arrays and calls the kernel once per block. The kernel loops over the cells in parallel. For each cell it finds the `n_up`-th largest value with `np.partition`. It sorts the genes above that value with a stable sort, then fills the last ranks with tied genes in gene order. Each set score uses the same area formula in a short closed form: `m * n_up - sum(ranks)`.

The output stays identical. The ranks are the same ordinal ranks that `rankdata` gives, because ties keep the gene order. Cells with NaN values still score zero, as before.

## Results

Median time of `ov.es.aucell(..., engine="cpu")` on one CPU core:

| Situation | Before | After | Change |
|---|---|---|---|
| 20 x 20 (test fixture size) | 3.41 ms | 2.77 ms | 19% faster |
| 1,600 x 3,000 dense, default `n_up` | 289.0 ms | 119.3 ms | 59% faster |
| 1,200 x 2,500 sparse CSR, `n_up=180` | 227.9 ms | 66.5 ms | 71% faster |
| 5,000 x 2,000 sparse CSR, default `n_up` | 892.9 ms | 226.7 ms | 75% faster |
| 300 x 3,000 dense, `n_up` = all genes | 60.6 ms | 38.1 ms | 37% faster |

When `n_up` equals the number of genes, the top-`n_up` selection skips no work. This case gains the least, and it is still not slower.

## Why this is safe and easy to maintain

The change touches only `_auc` and `_func_aucell`, and it keeps one code path for dense and sparse input. The scores are bit-for-bit equal to the old code, including ties, NaN rows and the `n_up` errors. The tests in `tests/test_es_methods.py` cover `ov.es.aucell` and the `ov.es.decoupler(method="aucell")` dispatcher.

## Validation

- Benchmark: dense 1,600 x 3,000 and CSR 1,200 x 2,500 count matrices, the test fixture, a DataFrame input and the dispatcher, all on one core. The time went from 803 ms to 334 ms in three separate runs (ratios 0.422, 0.416, 0.417). Each run also checked that all outputs match the unmodified code exactly.
- Tests: `pytest tests/test_es_methods.py -k "aucell or test_decoupler_dispatcher" -q` gives 2 passed, 12 deselected (same as `master`).
- Reproduce: `NUMBA_NUM_THREADS=1 pytest tests/test_es_methods.py -k aucell -q --durations=5`

## AI assistance

This PR was prepared with AI assistance from Aiden. Candidates were tracked with Weco Observe.

Weco share link: https://dashboard.weco.ai/share/-MxWBqeAys6SDW6tXOfmcjx2wkOiYy_h

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d94cf1da2d71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.