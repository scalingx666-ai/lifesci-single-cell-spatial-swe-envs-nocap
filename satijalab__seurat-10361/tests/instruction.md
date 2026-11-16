# Issue

**Title:** Fix NaN values being propagated by PrepSCTFindMarkers() in SCT Assays

## Description

Fixes 

Previously, when running SCTransform followed by PrepSCTFindMarkers() on multi layer Seurat objects, PrepSCTFindMarkers would incorrectly propagate genes with NaN fitted SCT parameters into the recorrection step. For instance, a Seurat object with an SCT assay split into a CTRL and a STIM layer, it is possible for only cells of the STIM layer to have significant expression of certain genes. As seperate SCT models are fit per layer per assay, this would mean cells of the CTRL layer would have NaN parameters during SCT fitting:

**Only cells of the STIM layer have significant expression for TGM1**
<img width="286" height="165" alt="image" src="https://github.com/user-attachments/assets/5306bca9-dc07-4b4a-8e82-92ac1a901a54" />

**models_pars_fit (parameters for the SCT model fit on each layer) can be NaN, in this case the AP006222.2 gene has a NaN fit value for SCT model1.1**
<img width="1171" height="170" alt="image" src="https://github.com/user-attachments/assets/dfe845e2-43ac-4df7-bcd3-8f1ec9eb97fe" />

Genes with NaN (Intercept) values would pass on NaN values into SCT counts and data layers, resulting in major downstream problems, such as FindMarkers() silently omitting affected genes, or FeaturePlot() simply failing to plot NaN expression values. This is a major issue for genes which are expressed only in certain conditions and not others; prior to these changes, these genes would be fully omitted from FindMarkers().

This PR addresses this issue by updating per-model recorrection step inside PrepSCTFindMarkers(). Before calling correct_counts(), the function now restricts recorrection to genes that have finite fitted SCT model params. Genes excluded from this step are then added back as zero rows, to preserve the full feature set. With these changes, PrepSCTFindMarkers() should no longer introduce NaN values for genes with non finite fits in multi layer SCT workflows. 

Reproducible example: 
```
library(Seurat)
library(SeuratData)

data("ifnb")
ifnb <- UpdateSeuratObject(ifnb)
ifnb <- subset(ifnb, subset = seurat_annotations == "CD14 Mono")
Idents(ifnb) <- ifnb$stim

# Object 1, single layer
x1 <- SCTransform(ifnb, min_cells = 0, return.only.var.genes = FALSE, verbose = FALSE)

# FindMarkers should return 14053 markers found
nrow(FindMarkers(x1, ident.1 = "STIM", ident.2 = "CTRL", assay = "SCT",
                 min.pct = 0, logfc.threshold = 0, test.use = "wilcox"))

# Object 2, multi layer after split 
x2 <- ifnb
x2[["RNA"]] <- split(x2[["RNA"]], f = x2$stim)
x2 <- SCTransform(x2, min_cells = 0, return.only.var.genes = FALSE, verbose = FALSE)
x2 <- PrepSCTFindMarkers(x2)
# Found 2 SCT models. Recorrecting SCT counts using minimum median counts: 2378

nrow(x2[["SCT"]])

# FindMarkers should still return 14053 markers with these changes
# Without these changes, FindMarkers would miss 253 markers 
# These markers are genes that have NaN in one layer's SCT but not the other
nrow(FindMarkers(x2, ident.1 = "STIM", ident.2 = "CTRL", assay = "SCT",
                 min.pct = 0, logfc.threshold = 0, test.use = "wilcox"))
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f3000d09e161`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.