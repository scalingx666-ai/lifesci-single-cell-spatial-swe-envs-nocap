# Issue

**Title:** perf(pl): draw chromosome heatmaps with infercnvpy's own numba renderer

## Description

Summary: `pl.chromosome_heatmap` and `pl.chromosome_heatmap_summary` are now drawn by infercnvpy itself instead of `scanpy.pl.heatmap`, so they stay fast and light at hundreds of thousands of cells while looking like before. On the 10x Atera breast FFPE data (154k cells), the heatmap takes 0.5 s and 0.6 GB instead of 29 s and 15 GB. At 661k cells, the previous code ran out of memory at 64 GB, while the new one takes 0.6 s and 1.4 GB.

Changes:
- New `mode` argument:
  - `mode="fast"` (default) is the new engine.
  - `mode="legacy"` is the previous implementation through `sc.pl.heatmap`, kept verbatim in `pl/_chromosome_heatmap_legacy.py`.
- How fast mode draws:
  - A figure has far fewer pixel rows than cells. Fast mode sorts the cells by group and assigns each group pixel rows in proportion to its size.
  - By default (`aggregate="sample"`), it draws one cell per pixel row, which is what the full-resolution plot shows after downscaling. The colour scale comes from all cell values, so it looks like the previous figure.
  - `aggregate="mean"` instead averages the cells of each pixel row, with the colour scale from the range of the averaged rows.
  - Both read the CNV matrix through one parallel numba kernel (CSR or dense) without densifying it. Dask and backed matrices are read block by block.
- Arguments from `sc.pl.heatmap`:
  - Fast mode implements `swap_axes`, `standard_scale`, `var_group_rotation`, `dendrogram`, `vmin`, `vmax`, `vcenter`, `norm` and `log` natively.
  - Any other argument logs an info line and switches to `mode="legacy"`, so existing calls keep working.
- Order and layout:
  - Both modes now keep the original cell order within each group. Before, it came from an unstable pandas sort and could differ between machines.
  - The summary keeps the category order. The previous code sorted groups alphabetically, so colours stored in `adata.uns` could end up on the wrong groups.
  - With `swap_axes`, the chromosome labels are drawn aligned. The previous strip was shifted by one window per chromosome.
  - Without a stored dendrogram, fast mode clusters the group mean profiles. A stored `uns["dendrogram_<groupby>"]` gives the same order as legacy.
- New `ax`, `return_fig` and `n_jobs` arguments.
- `save` now uses plain `fig.savefig` with scanpy's file naming, so the private `scanpy.plotting._utils.savefig_or_show` import is gone from the fast path.
- The image baselines are regenerated (same look). `docs/large_data.md` has a new plotting section.

Benchmark (HMGU cluster, 16 cores, X_cnv as CSR, plot plus savefig):

| data | legacy | fast, sample | fast, mean |
|---|---|---|---|
| Atera breast FFPE, 153,790 cells x 1521 windows | 29.3 s, 15.4 GB | 0.5 s, 0.63 GB | 0.7 s, 0.66 GB |
| Atera cervix, 660,964 cells x 1521 windows | out of memory at 64 GB | 0.6 s, 1.4 GB | 0.7 s, 1.5 GB |

Testing: New tests compare the numba kernels with numpy (dense, CSR, CSC, uneven and empty groups), check that fast and legacy draw identical values and colour scales when every cell gets its own row (also with `standard_scale` and `log`), and cover mean mode, the fallback to legacy, dask input, `ax`, `return_fig`, `save` and the dendrogram order. The full suite passes on the cluster (286 passed, 12 skipped), and so do prek and mypy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d95528b1d2e5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.