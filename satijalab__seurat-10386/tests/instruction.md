# Issue

**Title:** Add `uwot.init` parameter to `RunUMAP` to customize initialization

## Description

# Summary

Introduces parameter `uwot.init` for customizing initialization of UMAP, passed to `uwot::umap` or `uwot::umap2` (depending on `umap.method`). From the `uwot` docs:

> Options are:
> "spectral" Spectral embedding using the normalized Laplacian of the fuzzy 1-skeleton, with Gaussian noise added.
> "normlaplacian". Spectral embedding using the normalized Laplacian of the fuzzy 1-skeleton, without noise.
> "random". Coordinates assigned using a uniform random distribution between -10 and 10.
> "lvrandom". Coordinates assigned using a Gaussian distribution with standard deviation 1e-4, as used in LargeVis (Tang et al., 2016) and t-SNE.
> "laplacian". Spectral embedding using the Laplacian Eigenmap (Belkin and Niyogi, 2002).
> "pca". The first two principal components from PCA of X if X is a data frame, and from a 2-dimensional classical MDS if X is of class "dist".
> "spca". Like "pca", but each dimension is then scaled so the standard deviation is 1e-4, to give a distribution similar to that used in t-SNE. This is an alias for init = "pca", init_sdev = 1e-4.
> "agspectral" An "approximate global" modification of "spectral" which all edges in the graph to a value of 1, and then sets a random number of edges (negative_sample_rate edges per vertex) to 0.1, to approximate the effect of non-local affinities.
> A matrix of initial coordinates.

In previous discussions ` ` it's been pointed out that using the `"agspectral"` initialization option can produce better results for data of certain structure, e.g. when the default initialization produces a graph with disconnected components, causing issues with convergence (long runtimes and possible segfaults).

## Type of change
Bug fix (non-breaking change fixing an issue)

## Tests & examples
```r
# ensure you are working off of this branch
devtools::load_all(".")
library(SeuratData)
data("pbmc3k")
pbmc3k.final <- UpdateSeuratObject(pbmc3k.final)
p <- RunUMAP(pbmc3k.final, dims=1:10, uwot.init = "agspectral")
```

## Related issues
` `
(should confirm whether using this option / passing "agspectral" is able to solve the reported issues)

## Checklist
<!-- Ensure all items are complete before submitting -->

- [x] Branch is named appropriately (`feat/*`, `fix/*`, `docs/*`)
- [x] Code follows Seurat [style guidelines](https://github.com/satijalab/seurat/wiki/Contributor%27s-Guide)
- [x] Documentation and comments have been updated
- [x] `devtools::document()` has been run
- [x] `devtools::check()` passes with no errors or warnings

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d328fe91e890`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.