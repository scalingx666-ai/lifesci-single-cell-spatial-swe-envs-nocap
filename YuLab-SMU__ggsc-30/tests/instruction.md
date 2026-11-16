# Issue

**Title:** The features of sc_feature and sc_spatial can be specified the variables from colData or reduction result

## Description

## sc_feature

```
sc_feature(sce, features=c('PC1', 'sizeFactor'), reduction='TSNE', geom=geom_bgpoint, common.legend=F)
```

![image](https://github.com/user-attachments/assets/57a34c4e-da42-44b0-a7a9-c42fe51327a1)

## sc_spatial

```
sc_spatial(spe, features="cell_count", image.rotate.degree = -90, image.mirror.axis = NULL)
```
![image](https://github.com/user-attachments/assets/bc9758a3-d8d8-4687-82ba-079c6f10594e)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e9261e4fdef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.