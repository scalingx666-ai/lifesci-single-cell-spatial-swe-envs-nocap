# Issue

**Title:** Fix/run slsi.std assay no npcs binding

## Description

Drops reference to `npcs` variable from `RunSLSI.StdAssay`. Since `npcs` is not defined, the following NOTE to be thrown during CRAN checks:

```
❯ checking R code for possible problems ... [40s/40s] NOTE
  RunSLSI.StdAssay: no visible binding for global variable ‘npcs’
  Undefined global functions or variables:
    npcs
```

In lieu of any tests, the following script can be used to quickly verify `RunSLSI` is still working as expected:

```R
library(Seurat)
library(Signac)
library(BPCells)

# Convert "peaks" to an `Assay5` instance.
atac_small[["peaks"]] <- as(atac_small[["peaks"]], Class = "Assay5")
# `RunSLSI` should not raise any errors when passed a `StdAssay`.
atac_small <- RunSLSI(
  atac_small,
  graph = "peaks_snn",
  assay = "peaks"
)

# The same should be true for an `Assay5` instance holding a
# `BPCells::IterableMatrix`.
atac_small[["peaks"]]$data <- as(
  atac_small[["peaks"]]$data,
  Class = "IterableMatrix"
)
atac_small <- RunSLSI(
  atac_small,
  graph = "peaks_snn",
  assay = "peaks"
)
```

Relates to:
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af3cbc2f6c30`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.