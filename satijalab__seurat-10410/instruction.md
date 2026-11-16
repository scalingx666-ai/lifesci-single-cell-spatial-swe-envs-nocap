# Issue

**Title:** Fix genes being set to zero counts in PrepSCTFindMarkers for multi-SCT model objects

## Description

In a fix for a previous bug (#10361) where genes with NaN SCT parameters were being incorrectly left out of downstream FindMarkers and visualization steps, valid genes would sometimes incorrectly have their counts set to zero. 

Previously, PrepSCTFindMarkers() filtered genes prior to recorrection by requiring theta, (Intercept), and log_umi parameters to all be finite. This unintentionally removed genes with theta = Inf even when (Intercept) and log_umi were valid. 

For instance, in the below SCTModel.list, genes HMGN2 and AK2 in a multi-SCT model object would have their corrected counts set to 0 for model1:

```
[1] "model1"
           gene     theta intercept  log_umi  keep before after
HMGN2     HMGN2       Inf -10.94026 2.302585 FALSE     98     0
AK2         AK2       Inf -11.22116 2.302585 FALSE     73     0
CDK11B   CDK11B 0.1568015 -11.77633 2.302585  TRUE     39    39
PLEKHM2 PLEKHM2 0.3541736 -11.06855 2.302585  TRUE     84    84
[1] "model1.1"
           gene     theta intercept  log_umi  keep before after
HMGN2     HMGN2 0.2618025 -11.46332 2.302585  TRUE     61    61
AK2         AK2 0.2448065 -11.52153 2.302585  TRUE     54    54
CDK11B   CDK11B       Inf -12.13767 2.302585 FALSE     32     0
PLEKHM2 PLEKHM2       Inf -11.19668 2.302585 FALSE     81     0
```

This PR keeps genes with theta = Inf when mean model parameters are valid, while still excluding genes that produce NaN correct_counts().

Reproducible example: 
```
library(Seurat)
library(SeuratData)
library(Matrix)

#Load small ifnb subset
data("ifnb")
ifnb <- UpdateSeuratObject(ifnb)
ifnb <- subset(ifnb, subset = seurat_annotations == "CD14 Mono")

#Create a multi layer RNA assay
x <- ifnb
x[["RNA"]] <- split(x[["RNA"]], f = x$stim)
x <- SCTransform(
  x,
  min_cells = 0,
  return.only.var.genes = FALSE,
  verbose = FALSE
)

#These genes are erroneously set to zero counts
genes <- c("HMGN2", "AK2", "CDK11B", "PLEKHM2")

#Compare SCT counts before and after PrepSCTFindMarkers
before <- x
after <- PrepSCTFindMarkers(x)

models <- slot(before[["SCT"]], "SCTModel.list")

for (m in names(models)) {
  cells <- rownames(slot(models[[m]], "cell.attributes"))
  fa <- slot(models[[m]], "feature.attributes")
  
  before_counts <- GetAssayData(
    before,
    assay = "SCT",
    layer = "counts"
  )[, cells]
  
  after_counts <- GetAssayData(
    after,
    assay = "SCT",
    layer = "counts"
  )[, cells]
  
  genes_present <- intersect(genes, rownames(fa))
  
  #When looking at SCTModel parameters for genes of interest, "before" and "after" should be identical (ie: no genes erroneously filtered out)
  cat("\nSCT model:", m, "\n")
  print(data.frame(
    gene = genes_present,
    theta = fa[genes_present, "theta"],
    intercept = fa[genes_present, "(Intercept)"],
    log_umi = fa[genes_present, "log_umi"],
    passes_current_filter =
      is.finite(fa[genes_present, "theta"]) &
      is.finite(fa[genes_present, "(Intercept)"]) &
      is.finite(fa[genes_present, "log_umi"]),
    nonzero_before_prep = Matrix::rowSums(
      before_counts[genes_present, , drop = FALSE] > 0
    ),
    nonzero_after_prep = Matrix::rowSums(
      after_counts[genes_present, , drop = FALSE] > 0
    )
  ))
}
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d69e0f4ddd7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.