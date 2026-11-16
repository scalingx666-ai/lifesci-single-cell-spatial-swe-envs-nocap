# Issue

**Title:** Fixing #10354 with informative error

## Description

# Summary
This PR adds an explicit check for missing HVF information and stops with a more informative error message explaining that `VariableFeaturePlot()` cannot be generated in this situation.

## Type of change
<!-- Check the relevant option -->
- [x] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (existing functionality changed or removed)
- [ ] Documentation update
- [ ] Other (please explain below)

## Motivation
As described by Elaude in #10354, `HVFInfo()` returns `NULL` when global HVF information is requested after splitting layers, running `FindVariableFeatures()`, and subsequently joining layers. This currently results in an uninformative error in `VariableFeaturePlot()`.

## Tests & examples
<!-- Provide reproducible examples demonstrating the functionality -->
<!-- Include example code using built-in (pbmc_small) or readily available (SeuratData, etc.) datasets -->

```r
# Code from the seurat integration vignette:
obj <- LoadData("pbmcsca")
obj <- subset(obj, nFeature_RNA > 1000)
obj[["RNA"]] <- split(obj[["RNA"]], f = obj$Method)

obj <- NormalizeData(obj)
obj <- FindVariableFeatures(obj)
obj <- ScaleData(obj)
obj <- RunPCA(obj)
obj <- JoinLayers(obj) # Works without split, but not after
plot1 <- Seurat::VariableFeaturePlot(obj, assay = "RNA") # Doesn't work
```

## Related issues


## Checklist

- [x] Branch is named appropriately (`feat/*`, `fix/*`, `docs/*`)
- [x] Code follows Seurat [style guidelines](https://github.com/satijalab/seurat/wiki/Contributor%27s-Guide)
- [x] Documentation and comments have been updated
- [ ] `devtools::document()` has been run
- [ ] `devtools::check()` passes with no errors or warnings
- [ ] Test case demonstrating new functionality is included
- [x] Maintainers are allowed to edit this PR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `756343299869`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.