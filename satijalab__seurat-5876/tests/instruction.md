# Issue

**Title:** Suggestion: jitter & shuffle defaults FeatureScatter

## Description

Hi Seurat Team,

Just wanted to pop in potential suggestion for change in defaults on `FeatureScatter` based on recent issue #5875 where the jitter default can give false impression of data.  In looking at this I started wondering whether changing the default behavior from `jitter = TRUE` and `shuffle = FALSE` might actually be more informative for the user.  I'll describe my rationale and leave examples below and then leave it to your team.  As I say just potential suggestion and I likely do not have the full rationale for the design choices so feel free to reject the PR.

In most cases on truly crowded plot the `jitter` being applied doesn't (at least to my eye) significantly alter the visualization.  However, setting `shuffle = TRUE` does significantly alter things by reducing identity layering effects which can mask cell/identity location.  I do concede that the interpretability of the shuffled plot is also difficult due to sheer number of points but overall I think the effect is better than `shuffle = FALSE`.

Using the SeuratData hcabm40K as moderately (compared to 100K+ cells at least) crowded dataset.  I also cropped axes of plots below to increase resolution to see an effect of these parameters as raw dataset has some outliers.  

Thanks again for everything you do!

Best,
Sam

```
library(tidyverse)
library(Seurat)
library(scCustomize)
library(patchwork)

hcabm40k <- hcabm40k.SeuratData::hcabm40k

hcabm40k <- Add_Mito_Ribo_Seurat(seurat_object = hcabm40k, species = "human")

p1 <- FeatureScatter(object = hcabm40k, cols = DiscretePalette(palette = "polychrome", n = 36), feature1 = "nCount_RNA", feature2 = "percent_mito", pt.size = 0.75, jitter = T) + NoLegend() + xlim(0, 75000) + ylim(0, 10)

p2 <- FeatureScatter(object = hcabm40k, cols = DiscretePalette(palette = "polychrome", n = 36), feature1 = "nCount_RNA", feature2 = "percent_mito", pt.size = 0.75, jitter = F) + NoLegend() + xlim(0, 75000) + ylim(0, 10)

wrap_plots(p1, p2)
```

![image](https://user-images.githubusercontent.com/38284410/164532879-468f082e-8aa8-40dd-bcdd-927bd535a896.png)


```
p3 <- FeatureScatter(object = hcabm40k, cols = DiscretePalette(palette = "polychrome", n = 36), feature1 = "nCount_RNA", feature2 = "percent_mito", pt.size = 0.75, shuffle = F) + NoLegend() + xlim(0, 75000) + ylim(0, 10)

p4 <- FeatureScatter(object = hcabm40k, cols = DiscretePalette(palette = "polychrome", n = 36), feature1 = "nCount_RNA", feature2 = "percent_mito", pt.size = 0.75, shuffle = T) + NoLegend() + xlim(0, 75000) + ylim(0, 10)

wrap_plots(p3, p4)
```

![image](https://user-images.githubusercontent.com/38284410/164533103-aad64b84-e6b7-4ced-a4c3-ce3c4bff2252.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31895ef43a18`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.