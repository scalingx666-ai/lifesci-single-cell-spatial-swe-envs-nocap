# Issue

**Title:** update sc_dim and sc_violin

## Description

+ check the default mapping in `sc_dim` and `sc_violin`


```
> library(scuttle)
> library(scater)
> library(scran)
> library(ggplot2)
> library(ggsc)
> sce <- mockSCE()
> sce <- logNormCounts(sce)
> clusters <- clusterCells(sce, assay.type = 'logcounts')
> colLabels(sce) <- clusters
> sce <- runUMAP(sce, assay.type = 'logcounts')
> set.seed(123)
> genes <- rownames(sce) |> sample(6)
> sc_violin(sce, genes[1], slot = 'logcounts')
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/eb42795a-fd55-4aa8-84be-36530950b423)

```
> sc_violin(sce, genes[1], slot = 'logcounts',
       .fun=function(d) dplyr::filter(d, value > 0)
       ) +
       ggforce::geom_sina(size=.1)
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/9b2d8d60-26b3-4dc4-b110-cc2743f7a1e3)

```
sc_violin(sce, genes, slot='logcounts', mapping=aes(x = Cell_Cycle, fill = Cell_Cycle))
```
![abbf6db687bc491ef4d611bbf2409cb](https://github.com/YuLab-SMU/ggsc/assets/17870644/9e557b6b-465e-4183-8816-caa82506f9bc)

```
sc_violin(sce, genes, slot='logcounts', mapping=aes(fill = Cell_Cycle))
```
![80ef776a8f2d633eeaa47937c87cc5e](https://github.com/YuLab-SMU/ggsc/assets/17870644/32bd17dd-4b32-4f46-b6b3-67c1d449400e)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `92e2504d1877`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.