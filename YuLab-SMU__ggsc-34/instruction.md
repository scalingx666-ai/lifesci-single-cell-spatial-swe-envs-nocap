# Issue

**Title:** add plot_lisa_feature

## Description

add `plot_lisa_feature` to simplify the visualization of `LISA` result.


```
library(ggplot2)
library(SingleCellExperiment) |> suppressPackageStartupMessages()
library(SpatialExperiment) |> suppressPackageStartupMessages()
library(STexampleData)
# create ExperimentHub instance
eh <- ExperimentHub()
# query STexampleData datasets
myfiles <- query(eh, "STexampleData")
ah_id <- myfiles$ah_id[myfiles$title == 'Visium_humanDLPFC']
spe <- myfiles[[ah_id]]
spe <- spe[, colData(spe)$in_tissue == 1]
spe <-scater::logNormCounts(spe)
genes <- c('MOBP', 'PCP4', 'SNAP25', 'HBB', 'IGKC', 'NPY')
target.features <- rownames(spe)[match(genes, rowData(spe)$gene_name)]
library(SVP)
lisa.res1 <- runLISA(spe,
                     assay.type='logcounts',
                     features=target.features[seq(2)],
                     weight.method='knn',
                     k=50)
library(ggsc)
plot_lisa_feature(spe, lisa.res=lisa.res1, features=target.features[seq(2)],
                  pointsize=2, hlpointsize=2, gap_line_width=.1)
}
```

![image](https://github.com/user-attachments/assets/6bd175b2-a4f2-47b7-96b7-777a645f8cfd)

```

library(Seurat)
pbmc <- readRDS("./pbmc_seurat.rds")

features = c("MS4A1", "GNLY", "CD3E",
            "CD14", "FCER1A", "FCGR3A",
            "LYZ", "PPBP", "CD8A")

sce.pbmc <- as.SingleCellExperiment(pbmc)
library(SVP)
lisa.res2 <- runLISA(sce.pbmc, assay.type='logcounts', features = features,
                     reduction.used='UMAP', weight.method='knn', k=50)

plot_lisa_feature(sce.pbmc, lisa.res2, pointsize=.8, hlpointsize=.6, reduction='UMAP')
```

![image](https://github.com/user-attachments/assets/611af517-1520-4266-8856-cb3bd3a6670c)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17fe2323bb6b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.