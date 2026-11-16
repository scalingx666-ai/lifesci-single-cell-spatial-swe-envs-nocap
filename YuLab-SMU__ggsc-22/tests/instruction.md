# Issue

**Title:** add background point layer in grid level to be compatable with the framework of ggsc

## Description

```
library(Seurat)
library(SingleCellExperiment) |> suppressPackageStartupMessages()
library(ggsc)
library(ggplot2)
library(SpatialExperiment)

seu.pbmc <- readRDS('./pbmc_seurat.rds')

p1 <- sc_dim(seu.pbmc, pointsize=3, alpha=.7,
             bg_color='black', bg_line_width=.2, gap_line_width=.1)

p2 <- sc_dim(seu.pbmc, mapping=aes(color=ident, bg_color=ident),
       pointsize=3, alpha=.7, bg_line_width=.2, gap_line_width=.1)


p3 <- sc_dim(seu.pbmc, mapping=aes(color=ident, bg_color=seurat_clusters),
             pointsize=3, alpha=.7, bg_line_width=.2, gap_line_width=.1)

p1 + p2 + p3
```
![捕获](https://github.com/YuLab-SMU/ggsc/assets/17870644/b8a10300-3e15-461a-a9a3-f9b474f462da)

```
f1 <- sc_feature(seu.pbmc, features="S100A9", pointsize = 2.5)

f2 <- sc_feature(seu.pbmc, features = 'S100A9', density = TRUE, pointsize = 2.5)

f3 <- sc_feature(seu.pbmc, features = 'S100A9', bg_colour = 'black', gap_line_width = .1, pointsize=2.5)

f4 <-  sc_feature(seu.pbmc, features = 'S100A9', bg_colour = 'black', density = TRUE, gap_line_width=.1, pointsize=2.5)

f5 <- sc_feature(seu.pbmc, features="S100A9",
                 mapping = aes(bg_colour = ident),
                 pointsize=2.5, gap_line_width=.1)

f6 <- sc_feature(seu.pbmc, features="S100A9", mapping = aes(bg_colour = ident),
                 pointsize=2.5, gap_line_width=.1, density=TRUE)

f1 + f2 + f3 + f4 + f5 + f6
```
![features](https://github.com/YuLab-SMU/ggsc/assets/17870644/58b3b4f0-3f97-43b6-8dcc-697227af2234)


```
spe <- readRDS('./spe_data.rds')


ff1 <- spe |> sc_spatial(features = 'ENSG00000168314', image.plot = F, pointsize=3.5)

ff2 <- ff1 +
       sc_geom_point(data = ggtree::td_filter(ground_truth=='WM'), pointsize = 3.5,
                     bg_colour = 'black', gap_line_width=.15)

ff1 + ff2
```
![spatial](https://github.com/YuLab-SMU/ggsc/assets/17870644/ff9cd5a0-1f9e-4ca3-8fe6-1716b964a2ba)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42894d0502d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.