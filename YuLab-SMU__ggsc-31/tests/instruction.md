# Issue

**Title:** sc_dim_geom_ellipse and sc_dim_geom_label can be added after sc_feature

## Description

`sc_dim_geom_ellipse` and `sc_dim_geom_label` can be added after `sc_feature`

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
  sc_dim_geom_ellipse(
     mapping = aes(group = RNA_snn_res.0.5),
  ) +
  sc_dim_geom_label(
     geom = shadowtext::geom_shadowtext,
     mapping = aes(label = RNA_snn_res.0.5),
     bg.color = 'white',
     size = 5
  )

```

![image](https://github.com/user-attachments/assets/94127bcb-1357-41d6-8af1-3c75c6c90ee3)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d0ca5f055f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.