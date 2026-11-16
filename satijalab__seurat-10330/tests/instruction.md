# Issue

**Title:** Fix SCTransform umi.assay incorrect source assay labels

## Description

Fixes: 

Previously, SCTransform.Seurat() was hard-coded to only updated the umi.assay field for the first entry in SCTModel.list:

```{R}
slot(object = slot(object = assay.data, name = "SCTModel.list")[[1]], name = "umi.assay") <- assay
```

For objects with multiple SCT models, such as those created from multiple samples or layers, the remaining models did not have their source assay updated correctly, which would remain at the default "RNA" source assay. This would cause issues with downstream functions such as PrepSCTFindMarkers.

This simple change updates umi.assay for every model in SCTModel.list, so all SCT models consistently record the assay used to run SCTransform(). With these changes, individual SCT models should now correctly have their source assay assigned following SCTransform(). 

Reproducible example: 
```{R}
data("pbmc_small")

# Create fake Seurat object with two samples
rna_counts <- LayerData(pbmc_small, assay = "RNA", layer = "counts")
obj <- CreateSeuratObject(counts = rna_counts)
obj$sample <- rep(c("sample1", "sample2"), length.out = ncol(obj))

# Create new "decontX" assay
obj[["decontX"]] <- CreateAssayObject(counts = rna_counts)
obj[["decontX"]] <- split(obj[["decontX"]], f = obj$sample)

# Run SCTransform
obj <- SCTransform(
  object = obj,
  assay = "decontX",
  ncells = ncol(obj),
  variable.features.n = 20,
  return.only.var.genes = FALSE,
  conserve.memory = FALSE
)

# Inspect resulting SCT assay
# With these changes, there should be two SCT models model1 and model1.1, both with the
# decontX source assay (rather than an incorrect RNA source assay)
SCTResults(obj, slot = "umi.assay")
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b012c4cdda6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.