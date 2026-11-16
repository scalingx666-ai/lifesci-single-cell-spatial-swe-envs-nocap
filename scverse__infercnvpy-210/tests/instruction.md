# Issue

**Title:** feat: spatial CNV layer (tl.smooth_cnv, tl.spatial_regions, pl.spatial_cnv) and a Xenium tutorial

## Description

Summary: This PR adds spatial support that works with any CNV method in infercnvpy. `tl.smooth_cnv` smooths a CNV matrix over the spatial neighbourhood graph, `tl.spatial_regions` makes per-cell labels spatially coherent, and `pl.spatial_cnv` shows CNV of a chromosome or region on the tissue. A new tutorial applies them to a public Xenium Prime 5K squamous lung carcinoma.

Changes:
- Graph: all functions read a graph from `adata.obsp`, by default `obsp["spatial_connectivities"]` as written by `squidpy.gr.spatial_neighbors_knn`. squidpy is not a dependency of infercnvpy.
- `tl.smooth_cnv`:
  - Each step replaces a cell's CNV profile by a weighted mean of itself and its neighbours. By default the cell counts as one more neighbour, which for binary graphs is the plain mean over the cell and its neighbours.
  - `n_hops` repeats the step.
  - Each step is one parallel numba kernel that reads CSR input in place.
  - The result goes to `obsm["X_cnv_smoothed"]` together with the chromosome positions, so `pl.chromosome_heatmap(use_rep="cnv_smoothed")` works.
- `tl.spatial_regions`:
  - Regularises any categorical per-cell labels (for example tumour/normal calls or CNV clusters) with a Potts prior on the graph, solved by iterated conditional modes. The fixed sweep order makes it deterministic.
  - The unary term is a label-flip penalty, or `-log p` from per-cell class probabilities.
  - Missing labels are filled from their neighbours.
- `pl.spatial_cnv`:
  - A thin wrapper of `sc.pl.embedding` on `obsm["spatial"]`.
  - It colours cells by the mean CNV of a chromosome or genomic range (`region="chr3"` or `"chr3:93_000_000-199_000_000"`), or by any obs column.
- `tl.infercnv` now also stores the genomic start and end of each window in `uns[key]["window_start"]` and `["window_end"]`, which `pl.spatial_cnv` needs to select regions.
- `docs/notebooks/spatial_xenium.ipynb`:
  - Uses Xenium Prime 5K data from Bilous et al. 2026 (doi:10.1038/s41592-026-03089-8): 64,872 cells, 5,001 genes. Only the expression table is read, lazily, from the public scverse S3 bucket.
  - Normal reference cells come from marker scores, because the data has no cell types.
  - Pipeline: infercnv, smooth_cnv, CNV clusters with cnv_score, spatial_regions, heatmaps and maps. The tumour regions show the 3p loss and 3q gain typical of squamous lung cancer.
  - The notebook was executed on the HMGU cluster, and its outputs are committed.
- API docs have new "Spatial" sections, plus bibliography entries for the related methods (InSituCNV, SlideCNA, STARCH, CalicoST, the Han 2026 benchmark).

Validation on simulated tissue (50k cells, 5,000 genes, a tumour region with eight arm-level events, normal cells infiltrating it, and normal epithelium outside the reference):

| median counts per cell | 50 | 100 | 200 | 300 |
|---|---|---|---|---|
| correlation with the true profile, raw | 0.14 | 0.21 | 0.31 | 0.38 |
| after `smooth_cnv`, 2 hops | 0.43 | 0.56 | 0.68 | 0.74 |
| tumour/normal AUROC, raw -> 2 hops | 0.55 -> 0.72 | 0.58 -> 0.86 | 0.65 -> 0.96 | 0.74 -> 0.98 |
| MCC of calls, smoothed -> + `spatial_regions` | 0.27 -> 0.30 | 0.50 -> 0.56 | 0.77 -> 0.82 | 0.87 -> 0.88 |

Smoothing gives the large gain, and `spatial_regions` adds a smaller one on top. On 50k cells, `smooth_cnv` takes about 0.02 s per hop and `spatial_regions` about 0.03 s.

Testing: New `tests/test_spatial.py` compares the smoothing kernel with a scipy reference (dense, CSR and CSC input, several self weights, 1 and 3 hops, a weighted graph with a diagonal and an isolated cell) and checks that the serial and parallel kernels agree. It checks that ICM reduces 15 % label noise on a grid to under 2 %, determinism, the probability mode, filling missing labels, and round trips through `chromosome_heatmap` and `spatial_cnv`. The suite passes on the cluster (270 passed, 12 skipped), and so do prek, mypy and the docs build with `-W`.

squidpy comes with the new optional `spatial` extra (`pip install "infercnvpy[spatial]"`); the functions themselves accept any graph in `adata.obsp`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b9141182826`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.