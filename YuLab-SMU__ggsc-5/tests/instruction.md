# Issue

**Title:** to be compatible with SingleCellExperiment

## Description

update the related `functions` to be compatible with `SingleCellExperiment` class

## sc_dim

```
 library(ggsc)
 library(Seurat)
 library(SingleCellExperiment)
 library(ggplot2)
 library(aplot)

 sce <- readRDS('./pancreas.data.sce.rds')
 
 features <- c('CD4__chr12', 'LYZ__chr12')

 sc_dim(sce, reduction = 'TSNE')
 p1 <- sc_dim(sce, reduction = 'TSNE')

 p2 <- p1 + sc_dim_geom_label()

 p3 <- p1 + sc_dim_geom_label(geom = shadowtext::geom_shadowtext, color='black', bg.color='white')

 p4 <- p1 + sc_dim_geom_feature(sce, 'CD4__chr12', color='black')

 p5 <- sc_dim(sce, alpha=.3, reduction = 'TSNE') + ggnewscale::new_scale_color() +
       sc_dim_geom_feature(sce, features, mapping=aes(color=features)) +
       scale_color_viridis_d()


 p6 <- p1 + sc_dim_geom_ellipse(level=0.95)

 selected <- c(1, 2)
 p7 <- p1 + sc_dim_sub(subset=selected, .column = 'label')

 p8 <- sc_dim(sce, color='grey', reduction = 'TSNE') +
       sc_dim_geom_sub(subset=selected, .column = 'label') +
       sc_dim_geom_label(
         geom = shadowtext::geom_shadowtext,
         mapping = aes(subset = label %in% selected),
         color='black', bg.color='white'
       )
 p1 + p2 + p3 + p4 + p5 + p6 + p7 + p8
```

![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/083eaa93-ca29-4a85-9e08-daaf980d5292)

## sc_feature

```
 f1 <- sc_feature(sce, features = 'CD4__chr12', reduction = 'TSNE')

 f2 <- sc_feature(sce, features = features, reduction = 'TSNE')

 f1 + f2

```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/b1e73d3f-6bcf-41a4-a62c-912fc3dcfbc6)

## sc_violin

```
 pp1 <- sc_violin(sce, 'CD4__chr12')
 pp2 <- sc_violin(sce, 'LYZ__chr12', .fun=function(d) dplyr::filter(d, value > 0)) + ggforce::geom_sina(size=.1)

 pp1 + pp2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/c6877396-654a-42c4-a23d-0d5ef6d7abfe)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d0942bbe72d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.