# Issue

**Title:** Fix error in `FindSpatiallyVariableFeatures` from use of `slot` in function cascade

## Description

Pass `layer` instead of `slot` to `FindSpatiallyVariableFeatures.Assay` call in `FindSpatiallyVariableFeatures`. 

Currently because the call uses `slot`, the default layer (`scale.data`) is used instead of the layer originally passed, resulting in an error if that layer is empty. See below (example from spatial vignette):

```R
> cortex <- FindSpatiallyVariableFeatures(cortex, 
+                                         assay = "predictions", 
+                                         selection.method = "moransi", 
+                                         features = rownames(cortex), 
+                                         r.metric = 5, 
+                                         layer = "data")
# Warning: Layer ‘scale.data’ is empty
# Error in `colnames<-`(x = `*tmp*`, value = paste0("MoransI_", colnames(x = svf.info))) : 
#  attempt to set 'colnames' on an object with less than two dimensions
> traceback()
# 6: stop("attempt to set 'colnames' on an object with less than two dimensions")
# 5: `colnames<-`(x = `*tmp*`, value = paste0("MoransI_", colnames(x = svf.info))) at preprocessing.R#4757
# 4: FindSpatiallyVariableFeatures.Assay(object = object[[assay]], 
       # slot = slot, features = features, spatial.location = tc, 
       # selection.method = selection.method, r.metric = r.metric, 
       # x.cuts = x.cuts, y.cuts = y.cuts, nfeatures = nfeatures, 
       # verbose = verbose, ...) at generics.R#244
# 3: FindSpatiallyVariableFeatures(object = object[[assay]], slot = slot, 
       # features = features, spatial.location = tc, selection.method = selection.method, 
       # r.metric = r.metric, x.cuts = x.cuts, y.cuts = y.cuts, nfeatures = nfeatures, 
       # verbose = verbose, ...) at preprocessing.R#4809
# 2: FindSpatiallyVariableFeatures.Seurat(cortex, assay = "predictions", 
       # selection.method = "moransi", features = rownames(cortex), 
       # r.metric = 5, layer = "data") at generics.R#244
# 1: FindSpatiallyVariableFeatures(cortex, assay = "predictions", 
       # selection.method = "moransi", features = rownames(cortex), 
       # r.metric = 5, layer = "data")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc1076533df5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.