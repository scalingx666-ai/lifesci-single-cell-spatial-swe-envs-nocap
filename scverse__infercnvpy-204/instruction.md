# Issue

**Title:** perf: numba kernels with lazy dask and backed input for tl.infercnv

## Description

Summary: `tl.infercnv` now runs in numba kernels and accepts dask arrays and backed AnnData objects, so it no longer densifies the expression matrix or starts worker processes. It takes the lazy input design of #192 by Stephen Williams, who is credited as co-author, and replaces its compute with numba kernels. This PR builds on #203, so it targets that branch. The default noise threshold now follows R inferCNV and no longer depends on `chunksize`.

Changes:
- Each block of cells goes through one numba kernel, with a CSR and a dense version. The kernel maps the input columns to genomic order without copying the matrix, computes the bounded log fold change against the reference minimum and maximum, clips it at `lfc_clip`, and computes the pyramid running mean of the kept windows from two prefix sums. It then subtracts the median of each cell and writes float32. `calculate_gene_values` is a numba kernel too, and it writes a float32 cells x genes matrix.
- The kernels run with `prange` on the main thread, and `n_jobs` sets the number of numba threads (default: all cores). A serial copy of each kernel runs on any other thread, so infercnvpy never starts numba threads inside a dask worker. On macOS, numba's `workqueue` threading layer aborts the process in that case. `process_map`, the progress bar and the `tqdm` dependency are gone.
- In-memory and backed matrices are processed in blocks of `chunksize` cells, and a dask array in its own blocks. By default, the blocks are read one after another (with the synchronous scheduler for dask), and the result is an in-memory CSR matrix. With `lazy=True`, or by default when a `distributed.Client` is active, the result of a dask array stays a dask array of CSR blocks built with `map_blocks`. For lazy input, the reference means come from one pass over the data, as in #192.
- New `noise_reference="reference"` (default) computes the noise band from the reference cells as R inferCNV does (`clear_noise_via_ref_mean_sd`). The band is the mean of the reference cells plus or minus `dynamic_threshold` times the mean of their per-cell standard deviations, and all cells are used when there are no reference cells. `noise_reference="all"` uses the standard deviation of all cells around 0. The per-chunk standard deviation is removed, so `chunksize` only bounds memory. The setting is recorded in `uns["cnv"]["params"]`.
- Adds `numba` as a dependency and a `dask` extra. `NumbaPerformanceWarning` is an error in the tests, and coverage skips the compiled functions. New docs page `docs/large_data.md`, adapted from #192.
- `tl.infercnv` takes scanpy 1.13's `use` and `out` arguments, like the other functions since #203. `layer`, `key_added` and `inplace` still work with a FutureWarning, and `out=True` returns the results. `adata.uns[...]["params"]` records `use` instead of `layer`. Warnings now point at the caller's line past the `scverse_misc.deprecated_arg` wrappers.

Behaviour changes for the release notes:
- The default noise threshold changes, so `X_cnv` has about twice as many entries that are not zero (maynard2020_3k: 2.9M instead of 1.5M). `noise_reference="all"` gives the previous result for data that fit in one chunk.
- `chunksize` no longer changes the result.
- `X_cnv` and the gene values are float32 instead of float64.
- With dask input and `lazy=True` (or an active `distributed.Client`), `X_cnv` is a dask array.
- The gene order on tied start positions is unchanged. #192 used a stable sort, which changed 454 entries of maynard2020_3k.

Testing:
- With `noise_reference="all"` and main run as one chunk, the result equals main on maynard2020_3k (11 reference categories, one, and none; CSR and dense) and on the oligodendroglioma data. There are 0 zero/non-zero flips, and the largest difference is 3e-8 and 6e-8. The gene values have the same NaN pattern, 0 flips and a largest difference of 8e-8 to 1.2e-7.
- New tests compare the kernels to a plain numpy implementation of the algorithm for eight input formats, both noise modes, one and two references and three window sizes. Other tests cover dask (dense, CSR blocks, layers, lazy output, both schedulers), backed h5ad (CSR and dense), `read_elem_lazy` and `read_lazy`, the number of reads per block, chunk size invariance and `n_jobs`.
- The full suite passes on the latest versions (237 passed, 12 skipped) and on the minimum versions (235 passed, 14 skipped). mypy, the pre-commit hooks and the docs build with `-W` pass.

Benchmarks: maynard2020_3k replicated to 30k cells (CSR, 56 % reference cells), on an 8-core M-series Mac. Wall time is the faster of two runs, and the memory column is the peak of the process.

| implementation | cells | input | threads | wall | CPU | peak memory |
|---|---|---|---|---|---|---|
| main | 30k | in memory | 1 | 119 s | 114 s | 4.0 GB plus a 5 GB worker |
| this PR | 30k | in memory | 1 / 8 | 11.0 s / 2.4 s | 11 s | 2.4 GB |
| this PR | 30k | backed h5ad | 8 | 3.4 s | 12 s | 1.7 GB |
| this PR | 30k | dask | 8 | 3.7 s | 12 s | 1.3 to 1.5 GB |
| main | 3k | in memory | 8 | 15.4 s | 14 s | 0.9 GB plus a 3.5 GB worker |
| this PR | 3k | in memory | 8 | 0.21 s | 0.8 s | 0.74 GB |

The first call compiles the kernels in about 3 seconds, and later processes load them from the numba cache in 0.3 seconds. Main was not run at 30k cells with 8 threads, because its worker processes would need about 30 GB.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac72948c7ff6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.