# Issue

**Title:** fix(pp): qc_gpu final filter uses cells/genes not counts

## Description

## Summary

. The GPU QC path (`qc_gpu`, Step 3 "Final Filtering") forwarded the cell/gene filter thresholds to RAPIDS-SingleCell using the **wrong keyword arguments** — `min_counts`/`max_counts` instead of `min_genes`/`max_genes`/`min_cells`/`max_cells`.

With the default `max_cells_ratio=1`, the buggy call collapsed to:

```python
rsc.pp.filter_genes(adata, max_counts=n_cells)
```

which removes any gene whose **total UMI count** exceeds `n_cells`. That silently deleted highly expressed canonical markers (`S100A8`, `S100A9`, `LYZ`, `FCGR3B`, `CSF3R`, `CD74`, `HBB`, …), so downstream DotPlot / CellTypist appeared to "miss" common markers. Only the GPU path was affected — the CPU / mixed paths already use `_filter_*_impl(min_genes=…, max_genes=…, min_cells=…, max_cells=…)`.

## Change

The four `rsc.pp.filter_*` calls now use the correct arguments, matching the CPU path and the rapids-singlecell API (which mirrors scanpy's `filter_cells(min_genes=…)` / `filter_genes(min_cells=…)`):

```python
rsc.pp.filter_cells(adata, min_genes=min_genes)
rsc.pp.filter_cells(adata, max_genes=int(max_genes_ratio*adata.shape[1]))
rsc.pp.filter_genes(adata, min_cells=min_cells)
rsc.pp.filter_genes(adata, max_cells=int(max_cells_ratio*adata.shape[0]))
```

`int(...)` matches the CPU path, which passes integer thresholds.

Thanks to @ZHDATA2 for the precise bug report and reproduction.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e954f986dd06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.