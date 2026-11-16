# Issue

**Title:** docs: tutorials re-executed with current defaults, reproducible tumour calls, method differences to R inferCNV

## Description

Summary: This PR updates the documentation after a review by four personas (a newcomer with a biology background, an analyst who uses R inferCNV, a biologist who reads the plots, and an scverse maintainer). Each notebook's prose was also checked against its printed outputs and figures. The tutorials now run on current versions and show current defaults. Each claim in their prose is backed by a printed number or a figure on the page.

Changes:
- Installation and quickstart:
  - pip comes first, and the uv tab shows `uv init` for users who aren't in a uv project yet.
  - The `dask` extra is listed.
  - The quickstart log-transforms the example data, which is normalized but not log-transformed. It also drops steps whose results it didn't use.
- Method page (`infercnv.rst`): "minor modifications" is replaced by a short list of differences to R inferCNV:
  - the optional `min_mean` gene filter;
  - a single reference subtraction before smoothing;
  - the noise filter on by default;
  - no HMM;
  - a 100-gene default window.
- `large_data.md`: the number of passes over the data includes the `min_mean` pass. The memory estimate of `X_cnv` depends on the kept fraction instead of an assumed 10 %, and the page notes that `smooth_cnv` returns a dense matrix.
- `pl.chromosome_heatmap` docstring: chromosome width is the number of windows, and the same `vmin`/`vmax` are needed to compare figures.
- 3k tutorial, re-executed with current versions:
  - Tumour clusters were a hard-coded list from an older Leiden run, which no longer matched after the switch to igraph and included clusters of normal stromal cells. They now come from a threshold derived from clusters of reference cells. The notebook prints the threshold and a table of cell types against calls.
  - Fibroblasts, endothelial cells and pericytes join the reference.
  - The prose matches the figures, and the notebook no longer silences all warnings.
- Oligodendroglioma example:
  - Retitled, because the page didn't show a comparison with the R heatmap. It links the R figure and names the shared features (1p/19q loss).
  - The R timing is dropped.
- Xenium tutorial, re-executed:
  - It runs `tl.infercnv(..., dynamic_threshold=None)` before `tl.smooth_cnv`, as the `smooth_cnv` docstring now recommends.
  - Raw and smoothed heatmaps share one colour scale.
  - Tumour calls compare a per-cell score with a per-cell threshold, and the share of non-epithelial calls is printed.
  - A table of calls replaces an agreement number that used the smoothed calls as the truth.
  - The install line includes all needed extras.
- README and 3k tutorial: the experimental warning is replaced by a short note that results look similar, but not identical, to those of R inferCNV.

Testing: All three notebooks were executed on the HMGU cluster with Python 3.13 and scanpy 1.12. The docs build passes with `-W -n`, and so does prek. A second, independent check of the prose against the new outputs found no remaining unsupported claims after the fixes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63e16cdcf791`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.