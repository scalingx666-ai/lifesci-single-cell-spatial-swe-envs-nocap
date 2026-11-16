# Issue

**Title:** colour mapping of sc_dim_geom_label and sc_dim_geom_ellipse work with sc_feature

## Description

This pr refines the #31 

```
library(Seurat)
library(ggsc)
library(ggplot2)
library(ggnewscale)

pbmc <- readRDS("./pbmc_seurat.rds")

features = c("MS4A1", "GNLY", "CD3E",
            "CD14", "FCER1A", "FCGR3A",
            "LYZ", "PPBP", "CD8A")

sc_feature(pbmc,
           mapping = aes(bg_colour = RNA_snn_res.0.5),
           features = features,
           reduction = 'umap',
           geom = geom_bgpoint,
           pointsize = 1
  ) +
  ggnewscale::new_scale_color() +
  sc_dim_geom_ellipse(
     mapping = aes(group = RNA_snn_res.0.5, colour=RNA_snn_res.0.5),
  ) +
  sc_dim_geom_label(
     geom = shadowtext::geom_shadowtext,
     mapping = aes(label = RNA_snn_res.0.5, colour = RNA_snn_res.0.5),
     bg.color = 'white',
     size = 5
  )
```
![image](https://github.com/user-attachments/assets/dacd408e-a998-408a-b8d0-fd180cfdd5f5)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `760ece20234b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.