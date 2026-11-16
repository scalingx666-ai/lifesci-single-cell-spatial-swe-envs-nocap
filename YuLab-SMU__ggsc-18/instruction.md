# Issue

**Title:** supporting plot pie for spatial data

## Description

plot pie for spatial data

```
> library(SpatialExperiment) |> suppressPackageStartupMessages()
> library(Seurat) |> suppressPackageStartupMessages()
> library(ggplot2)
> library(ggsc)
> spe <- readRDS('./spe_data.rds')
> seu <- readRDS('./brain.sru.rds')
> g1 <- rownames(spe) |> sample(10)
> g2 <- rownames(seu) |> sample(10)
> p1 <- spe |> sc_spatial(features=g1, plot.pie=T, pie.radius.scale=.3, linewidth=0.1, image.plot=F)
> p2 <- seu |> sc_spatial(features=g2, plot.pie=T, pie.radius.scale=.35, image.plot=F)
> p1 + p2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/60385470-79cb-4e1e-9ea3-a73bb77139b0)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b972dfb6e0f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.