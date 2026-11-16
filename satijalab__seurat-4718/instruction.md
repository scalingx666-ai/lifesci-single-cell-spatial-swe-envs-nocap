# Issue

**Title:** Update pbmc3k vignette: replace `top_n`

## Description

HI Seurat Team,

Very minor PR but helps future proof (and is more intuitive user facing).  Noticed in writing my own function recently that the `dplyr::top_n` function has been designated as "superseded" and while not deprecated in near future the functionality has been moved to `slice_max`.  `slice_max` has both a syntax advantage (using `order_by` instead of `wt`) and more intuitively orders the results output using the variable supplied to `order_by`.  I have updated the .Rmd file for the vignette to use `slice_max`.

Below is example with pbmc3k dataset demonstrating difference in results ordering between `top_n` and `slice_max` (*Edit: this was using Seurat 3.2.3 hence "avg_logFC" but works regardless of version since it's just data.frame filtering).

Best,
Sam


```
library(tidyverse)
library(Seurat)

pbmc <- pbmc3k.SeuratData::pbmc3k.final

markers <- FindAllMarkers(pbmc)

# Using top_n method
filtered_markers_top <- markers %>%
  rownames_to_column("rownames") %>%
  group_by(cluster) %>%
  top_n(n = 10, wt = avg_logFC) %>%
  column_to_rownames("rownames")

head(filtered_markers_top, 5)

              p_val avg_logFC pct.1 pct.2     p_val_adj     cluster  gene
LDHB  1.963031e-107 0.7300635 0.901 0.594 2.692101e-103 Naive CD4 T  LDHB
CCR7   1.606796e-82 0.9219135 0.436 0.110  2.203560e-78 Naive CD4 T  CCR7
CD3D   4.198081e-77 0.6598608 0.838 0.406  5.757249e-73 Naive CD4 T  CD3D
NOSIP  3.191555e-50 0.6926087 0.628 0.358  4.376899e-46 Naive CD4 T NOSIP
LEF1   3.324866e-49 0.7296372 0.336 0.104  4.559722e-45 Naive CD4 T  LEF1


# Using slice_max method
filtered_markers_slice <- markers %>%
  rownames_to_column("rownames") %>%
  group_by(cluster) %>%
  slice_max(n = 10, order_by = avg_logFC) %>%
  column_to_rownames("rownames")

head(filtered_markers_slice, 5)

                  p_val avg_logFC pct.1 pct.2     p_val_adj     cluster      gene
CCR7       1.606796e-82 0.9219135 0.436 0.110  2.203560e-78 Naive CD4 T      CCR7
LDLRAP1    7.374411e-30 0.7636255 0.245 0.084  1.011327e-25 Naive CD4 T   LDLRAP1
LDHB      1.963031e-107 0.7300635 0.901 0.594 2.692101e-103 Naive CD4 T      LDHB
LEF1       3.324866e-49 0.7296372 0.336 0.104  4.559722e-45 Naive CD4 T      LEF1
PRKCQ-AS1  2.498572e-44 0.7119736 0.331 0.110  3.426542e-40 Naive CD4 T PRKCQ-AS1
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `340b34891f8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.