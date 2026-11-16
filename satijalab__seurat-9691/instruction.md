# Issue

**Title:** Fix `SpatialDimplot(..., interactive = TRUE)` to support all `SpatialImage` types

## Description

This PR resolves an issue encountered when running `SpatialDimplot` on `SlideSeq` or `STARmap` inputs with `interactive = TRUE`. Since the functionality is interactive, implementing a proper test is a bit of a PITA so in lieu, the following script can be used to verify that the bug has been resolved:

```R
library(Seurat)
library(SeuratData)

test_case <- LoadData("ssHippo")
test_case <- AddMetaData(
  test_case, 
  metadata = runif(nrow(test_case), min = 1, max = 10),
  col.name = "random_labels"
)

SpatialDimPlot(test_case, group.by = "random_labels", interactive = TRUE)
```

The issue was introduced by yours truly in `Seurat` 5.1.0 when I . The trouble was that the `ScaleFactors` generic wasn't implemented for `SlideSeq` or `STARmap`, hence the error:

```
Error in UseMethod(generic = "ScaleFactors", object = object) : 
  no applicable method for 'ScaleFactors' applied to an object of class "c('SlideSeq', 'SpatialImage')"
```

The fix is to define the generic for the types in question, `ScaleFactors.SlideSeq` and `ScaleFactors.STARmap`. Both implementations return a `scalefactors` S3 class with all its values set to 1. Another alternative is to update `ISpatialDimPlot` to check the class of `object[[image]]` and conditionally call `ScaleFactors` on the appropriate types:

```R
  scale.factor <- 1
  if (inherits(object[[image]], c("VisiumV1", "VisiumV2"))){
    scale.factor <- ScaleFactors(object[[image]])[[image.scale]]
  }
```

My thinking is that although the `scalefactors` class is specific to the Visium platform (and therefore kinda "wrong" to populate for other technologies) we're eventually planning on unifying all of the `SpatialImage` implementations under the `FOV` class. Until then, it seems like a good idea to take the opportunity to refine the disparate types to expose a consistent interface. 

Reported as:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6d238c4f5394`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.