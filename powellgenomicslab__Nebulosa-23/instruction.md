# Issue

**Title:** Update plotting.R

## Description

Made change as described in  changed `plotting.R` as @pedriniedoardo suggested (`labs(color = guide_legend(legend_title)) +` to `labs(color = legend_title) +` on line 32), and `plot_density()` is now working as expected for me.

```
# Installing my fork of Nebulosa to test `plot_density`
library("devtools")
install_github("beigelk/Nebulosa")

library(Nebulosa)

pbmc = readRDS("~/test_data/pbmc_processed.Rds")
plot_density(pbmc, features = c("LYZ", "CD14"), joint = TRUE)
```
![image](https://github.com/powellgenomicslab/Nebulosa/assets/123108611/acada862-6143-4d50-a59c-25c062ee8776)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9d81a205340`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.