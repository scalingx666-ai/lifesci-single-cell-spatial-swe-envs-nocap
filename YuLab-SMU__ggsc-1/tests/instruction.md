# Issue

**Title:** fix a bug of sc_dim_geom_feature when reduction is not umap

## Description

when reduction is not 'umap', the sc_dim_geom_feature will generate an error because the data used in `sc_dim_geom_feature` is different from the data used in `sc_dim`.

```
> pbmc <- RunTSNE(pbmc, reduction='pca', dims=1:5)
> library(scplot)
> sc_dim(pbmc, reduction='tsne')
> sc_dim(pbmc, reduction='tsne') + sc_dim_geom_feature(object=pbmc,features='CD4')
Error:
! Problem while computing aesthetics.
ℹ Error occurred in the 2nd layer.
Caused by error in `FUN()`:
! object 'tSNE_1' not found
Run `rlang::last_error()` to see where the error occurred.
```

we can introduce `reduction` in `sc_dim_geom_feature`, but I think this pr may be better since the users do not need to provide `reduction` again.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb74885d48e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.