# Issue

**Title:** Feat/VisiumV1 return

## Description

Adds an `image.type` parameter to `Read10X_Image` allowing users to choose which class is returned: `VisiumV1` or `VisiumV2`. The behavior of the parameter is described in the following test script:

```R
library(testthat)
library(Seurat)

path_to_image <- "path/to/image/"

visium_default <- Read10X_Image(path_to_image)
expect_true(inherits(visium_default, "VisiumV2"))

visium_v1 <- Read10X_Image(path_to_image, image.type = "VisiumV1")
expect_true(inherits(visium_v1, "VisiumV1"))

visium_v2 <- Read10X_Image(path_to_image, image.type = "VisiumV2")
expect_true(inherits(visium_v2, "VisiumV2"))
```

Relates to:
- 
- 
- 
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c87c96d31b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.