# Issue

**Title:** Use `fill` when passed through `...` in `LabelClusters` for label box background color

## Description

Fix ability to specify `fill` for label box background color in `LabelClusters`; this .

[Previously: label box fill remained the default (cluster color) even when a value was passed, and produced warning `"Warning message: Duplicated aesthetics after name standardisation: fill"`.]

## Tests & examples

```r
# First make sure you’re on this branch 
devtools::load_all("~/seurat") # pak::pkg_install("satijalab/seurat@fix/labelclusters-box-fill")
plot <- DimPlot(pbmc_small)

# Default behavior - boxes are filled with the color assigned to the cluster
p1 <- LabelClusters(plot = plot, id = "ident", box = T)

# Specify white background for label box
p2 <- LabelClusters(plot = plot, id = "ident", box = T, fill = "white")

# Specify white background (with repel=F)
p3 <- LabelClusters(plot = plot, id = "ident", box = T, fill = "white", repel=F)

# Passing other arguments works as before
p4 <- LabelClusters(plot = plot, id = "ident", box = T, fill = "black", color = "lightgreen", size = 2)

p1 | p2 | p3 | p4
```
<img width="1000" height="200" alt="image" src="https://github.com/user-attachments/assets/31c5c836-c59b-40cb-b50e-1a4797e3e4e9" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7670bd4c6de2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.