# Issue

**Title:** fix(space): guard svg(mode='pearsonr') against all-zero spots

## Description

## Summary

 — `ov.space.svg(adata, mode='pearsonr', n_svgs=3000)` raises `ZeroDivisionError: division by zero` on Visium HD segmented data.

Pearson-residual HVG selection normalizes each spot by its total UMI count. Visium HD nucleus/cell **segmentation** produces segments that capture no reads (all-zero spots); dividing by their zero total count blows up inside scanpy's `_highly_variable_pearson_residuals` — raised as an error on the rapids-singlecell GPU path, and silently producing NaN residuals on CPU.

## Fix

Filter out all-zero spots from the throwaway `bdata` copy **before** calling `preprocess(..., mode='shiftlog|pearson')` — exactly the location suggested by the reporter (@hufanglq): *"we need to filter out all zero cells before call `_highly_variable_pearson_residuals`"*.

`bdata` exists only to pick genes; its `highly_variable` flags are mapped back to `adata` **by gene name**, so dropping empty spots there leaves the **returned AnnData's cells completely unchanged**. A short message reports how many spots were dropped.

## Verification

- Synthetic Visium-like data with all-zero spots (sparse **and** dense `X`): `svg(mode='pearsonr')` now completes, selects SVGs, and returns the full cell count (200 → 200) with 15 empty spots dropped only from the internal gene-selection copy.
- `flake8 --select=E9,F63,F7 omicverse/space/_svg.py` clean.

Thanks to @hufanglq for the precise diagnosis and suggested fix.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `25cf4fe214f7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.