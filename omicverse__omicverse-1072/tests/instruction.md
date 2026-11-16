# Issue

**Title:** CNV (copykat): use pycopykat 0.2.0 (same results as R copykat 1.2.5)

## Description

pycopykat 0.2.0 is now on PyPI (`pip install pycopykat`). From the same seed it gives R copykat 1.2.5's breakpoints and the same call for every cell; see omicverse/py-CopyKAT#8.

Changes in `ov.single.CNV(method="copykat")`:
- **Predictions:** read R's prediction columns (`cell.names`, `copykat.pred`), with a fallback to the old `cell` column.
- **Bins:** pycopykat now indexes bins by R's `chrom, chrompos, abspos`. The wrapper derives `start`/`end` for each bin in `uns['cnv']['bin_meta']`, so the heatmap's arm split keeps working.
- **Install hint:** now points to PyPI (`pycopykat>=0.2.0`). The guard test is updated to match.
- **`n_jobs` docstring:** the result does not depend on it.

I checked it on copykat's example data (302 cells). `obs['cnv_prediction']` equals R copykat's calls, and `obsm['X_cnv']` is 302 × 12,167.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cf9c80d8c92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.