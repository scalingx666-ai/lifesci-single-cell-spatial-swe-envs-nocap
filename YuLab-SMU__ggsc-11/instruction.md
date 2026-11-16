# Issue

**Title:** introduce joint to combine all features with joint.fun and speed up calculate of kde using parallel

## Description

+ `joint` argument control whether to combine the features with `joint.fun` .
+ using `RcppParallel` to speed up.

```
scale.color <- scale_color_viridis_c(option='B')

p1 <- sc_feature(pbmc, features="CD4", reduction='UMAP', density=T) + scale.color
p2 <- sc_feature(pbmc, features="CCR7", reduction = 'UMAP', density=T) + scale.color
p3 <- sc_feature(pbmc, features = "CD8A", reduction = 'UMAP', density = T) + scale.color
p4 <- sc_feature(pbmc, features = c("CD4", "CCR7", "CD8A"), reduction = 'UMAP', density = T, joint = TRUE) + scale.color
(p1 + p2 + p3) / p4                                       
```
![image](https://github.com/YuLab-SMU/ggsc/assets/17870644/2afc32eb-c782-4c4f-a3ec-a869c2fcce03)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2601bb0cde4c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.