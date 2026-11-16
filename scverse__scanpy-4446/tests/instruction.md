# Issue

**Title:** fix: avoid loading whole dask arrays in `axis_nnz` and `check_nonnegative_integers`

## Description

**LLM usage**

<!-- See the scverse AI policy: https://scverse.org/about/ai_policy/ -->

- [x] LLM or coding agent used: Claude Opus 5.5 via Claude Code
- [x] If one was used, I, a human, have reviewed, understood and tested every changed line
- [x] 
- [x] [Tests][] included or not required because: added `test_dask_reductions_blockwise` to `tests/test_utils.py`. It checks that every per-block call receives a single chunk. It fails on `main` for `check_nonnegative_integers` and `axis_nnz(axis=0)`.
- [ ] [Release notes][] not necessary because:

The dask implementations of `check_nonnegative_integers` and `axis_nnz` now use `da.reduction` instead of `map_blocks(..., drop_axis=...)`. Each block produces a small result, either a single bool or a vector of counts, and only those results are combined. The in-memory dtype is kept: `axis_nnz` returns int32 for scipy sparse, and `np.sum` would upcast to int64. This matters because `test_dask_against_in_memory` compares the dtypes.

Peak RSS for the script in #4445 (1.6 GB array, 80 MB chunks):

| call | `main` | this PR |
|---|---|---|
| `X.sum(axis=0).compute()` (reference) | 0.53 GB | 0.60 GB |
| `highly_variable_genes(flavor="seurat_v3")` | 5.38 GB | 0.78 GB |
| `calculate_qc_metrics` | 3.83 GB | 0.62 GB |
| `rank_genes_groups(method="t-test")` | 5.38 GB | 0.93 GB |

`tests/test_utils.py`, `tests/test_qc_metrics.py`, `tests/test_highly_variable_genes.py` and `tests/test_rank_genes_groups.py` all pass locally (Python 3.14).

[tests]: https://scanpy.readthedocs.io/page/dev/testing.html#writing-tests
[release notes]: https://scanpy.readthedocs.io/page/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afa0caf57144`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.