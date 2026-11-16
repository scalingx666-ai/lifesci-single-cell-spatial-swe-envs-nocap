# Issue

**Title:** Adding a utility function to subset RCTD/spacexr object based on spatial spot ids

## Description

Hi Spacexr team,

Thanks for the great tool! In some scenario I realize I want to subset the resulting RCTD/spacexr object based on the desired spatial barcode id to make the downstream processing smoother. So I wrote this simple subset function that essentially subset following 3 slots

1. @spatialRNA
2. @originalSpatialRNA
3. @results$weights
to match spots provided by user
a example using (using Visium seurat object) would be
```R
rctd_obj = readRDS('path/to/rctd_object.rds')
st_obj = readRDS('path/to/visium_seurat_object.rds')
spot_ids_keep = colnames(st_obj)[1:300]
rctd_obj_new = subset(rctd_obj, spot_ids_keep)
```

Hope this make sense and could benefit other user too. Please let me know if you have any questions or suggestions for improvement!

Thanks,

Simon

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8bc65f868b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.