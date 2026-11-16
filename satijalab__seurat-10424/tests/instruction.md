# Issue

**Title:** Fix behavior of `fill.by` / `y.max` / `same.y.lims` parameters in `RidgePlot`

## Description

## Summary

 by @samuel-marsh.

This PR proposes the following:

- Change the default value of the `fill.by` parameter.
  - The default value in the documentation was "feature", but due to overrides by `ExIPlot`, the default was actually "ident". Changing this to NULL, and picking a different default inside the function (ident if stack if FALSE, feature otherwise) helps to clarify this behavior.
- Compute y axis limits properly if `same.y.lims = TRUE`. Add noise as necessary, following logic in `MultiExIPlot`, then apply this to all plots.
- Add parameter `fill.by` to `SingleExIPlot`. The default is "ident" so complete backwards compatibility is maintained (across calls to this function, for example in other visualization functions).
- Apply the proper limits to the axis as requested.

## Reprex

``` r
suppressPackageStartupMessages({
  library(SeuratData)
  library(dplyr)
  library(patchwork)
})
#> Warning: package 'dplyr' was built under R version 4.5.2

# must be on this branch
devtools::load_all("~/seurat", quiet = TRUE)
#> Warning: package 'sp' was built under R version 4.5.2

pbmc <- suppressWarnings(suppressMessages(UpdateSeuratObject(pbmc3k.final))) %>% subset(seurat_annotations %in% c("Platelet", "DC", "CD8 T", "CD14+ Mono"))

# fill.by
# note that fill.by = "feature" is not informative unless stack = TRUE
RidgePlot(pbmc, features = "CD3E", fill.by = "ident") /
  RidgePlot(pbmc, features = "CD3E", fill.by = "feature")
#> Picking joint bandwidth of 0.0808
#> Picking joint bandwidth of 0.0808
```

![](https://i.imgur.com/mroG4HM.png)<!-- -->

``` r

# same.y.lims
RidgePlot(pbmc, features = c("CD3E", "LYZ"), same.y.lims = FALSE) /
  RidgePlot(pbmc, features = c("CD3E", "LYZ"), same.y.lims = TRUE)
#> Scale for x is already present.
#> Adding another scale for x, which will replace the existing scale.
#> Scale for x is already present.
#> Adding another scale for x, which will replace the existing scale.
#> Picking joint bandwidth of 0.0808
#> 
#> Picking joint bandwidth of 0.376
#> 
#> Picking joint bandwidth of 0.0808
#> 
#> Picking joint bandwidth of 0.376
#> Warning: Removed 1 row containing non-finite outside the scale range
#> (`stat_density_ridges()`).
```

![](https://i.imgur.com/UaP57Dx.png)<!-- -->

``` r

# y.max
RidgePlot(pbmc, features = "CCL5") /
  RidgePlot(pbmc, features = "CCL5", y.max = 3)
#> Picking joint bandwidth of 0.176
#> Picking joint bandwidth of 0.201
#> Warning: Removed 250 rows containing non-finite outside the scale range
#> (`stat_density_ridges()`).
```

![](https://i.imgur.com/Q8pb1cK.png)<!-- -->

``` r

# stacked fill.by
RidgePlot(pbmc, features = c("CCL5", "LYZ", "CD3E"), stack = TRUE, fill.by = "ident") /
  RidgePlot(pbmc, features = c("CCL5", "LYZ", "CD3E"), stack = TRUE, fill.by = "feature")
#> Picking joint bandwidth of 0.176
#> Picking joint bandwidth of 0.376
#> Picking joint bandwidth of 0.0808
#> Picking joint bandwidth of 0.176
#> Picking joint bandwidth of 0.376
#> Picking joint bandwidth of 0.0808
```

![](https://i.imgur.com/0MW8BVR.png)<!-- -->

``` r

# stacked same.y.lims
RidgePlot(pbmc, features = c("CCL5", "LYZ", "CD3E"), stack = TRUE, same.y.lims = TRUE)
#> Picking joint bandwidth of 0.176
#> Picking joint bandwidth of 0.376
#> Picking joint bandwidth of 0.0808
```

![](https://i.imgur.com/1Vii58H.png)<!-- -->

<sup>Created on 2026-07-13 with [reprex v2.1.1](https://reprex.tidyverse.org)</sup>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `621eb2d4867f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.