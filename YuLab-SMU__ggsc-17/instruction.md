# Issue

**Title:** add the meta.data of cell for Seurat

## Description

considering the meta.data of cell for `Seurat` object in `get_dim_data`

related #16 

```
> library(ggsc)
> pbmc.seut <- readRDS('./pbmc_seurat.rds')
> p <- pbmc.seut |> sc_dim()
> p$data |> head()
                     UMAP_1    UMAP_2        ident orig.ident nCount_RNA
AAACATACAACCAC-1   3.325538 -4.101189  Naive CD4 T     pbmc3k       2419
AAACATTGAGCTAC-1   4.449747 11.148801            B     pbmc3k       4903
AAACATTGATCAGC-1   6.016574 -6.904137 Memory CD4 T     pbmc3k       3147
AAACCGTGCTTCCG-1 -10.999634  4.242199 FCGR3A+ Mono     pbmc3k       2639
AAACCGTGTATGCG-1   5.014720  1.765654           NK     pbmc3k        980
AAACGCACTGGTAC-1   2.496269 -6.072399 Memory CD4 T     pbmc3k       2163
                 nFeature_RNA RNA_snn_res.0.5 seurat_clusters
AAACATACAACCAC-1          779               0               0
AAACATTGAGCTAC-1         1352               3               3
AAACATTGATCAGC-1         1129               2               2
AAACCGTGCTTCCG-1          960               5               5
AAACCGTGTATGCG-1          521               6               6
AAACGCACTGGTAC-1          781               2               2
> p2 <- pbmc.seut |> sc_dim(mapping=aes(color=seurat_clusters))
> p + p2
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/099898b3-9681-49be-a491-e064ee597570)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c02be5c303f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.