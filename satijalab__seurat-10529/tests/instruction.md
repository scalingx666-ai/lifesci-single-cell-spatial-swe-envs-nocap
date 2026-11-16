# Issue

**Title:** JackStraw(): Significant memory reduction in parallel processing => faster processing

## Description

# Summary

Reduce memory consumption for parallel processing in `JackStraw()`.

## Type of change
- [x] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (existing functionality changed or removed)
- [ ] Documentation update
- [x] Other (please explain below)

## Motivation

Decrease memory needs and improve performance.

## Tests & examples

```r
library(Seurat)
library(future)

# Standard workflow scale (2,000 features x 500 cells)
set.seed(42)
counts <- matrix(rpois(2000 * 500, lambda = 1), nrow = 2000, ncol = 500)
rownames(counts) <- paste0("gene", 1:2000)
colnames(counts) <- paste0("cell", 1:500)
obj <- CreateSeuratObject(counts = counts)
obj <- NormalizeData(obj, verbose = FALSE)
obj <- FindVariableFeatures(obj, verbose = FALSE)
obj <- ScaleData(obj, verbose = FALSE)
obj <- RunPCA(obj, verbose = FALSE)

plan(multisession, workers = 2)

# Record payload size exported to parallel workers
.sizes <- numeric(0)
trace("getFutureData", where = asNamespace("future"), print = FALSE,
  exit = quote({
    val <- returnValue()
    .sizes[length(.sizes) + 1] <<- length(serialize(val, NULL, xdr = FALSE))
  })
)

t <- system.time(suppressWarnings(JackStraw(obj, dims = 2, num.replicate = 5, verbose = FALSE)))[["elapsed"]]
untrace("getFutureData", where = asNamespace("future"))

# The last 2 chunks correspond to the empirical p-value step across 2 workers
emp_payload <- tail(.sizes, 2)
cat(sprintf("* Seurat %s: %.2fs elapsed, %.2f MB exported across workers\n",
            packageVersion("Seurat"), t, sum(emp_payload) / 1e6))
```

gives:

* Seurat 5.6.0: 7.61s elapsed, 68.42 MB exported across workers
* Seurat 5.6.0.9000: 2.23s elapsed, 1.68 MB exported across workers (3.4x faster, 40.6x less data)
 

## Related issues

Issue #10530

## Checklist
<!-- Ensure all items are complete before submitting -->

- [x] Branch is named appropriately (`feat/*`, `fix/*`, `docs/*`)
- [x] Code follows Seurat [style guidelines](https://github.com/satijalab/seurat/wiki/Contributor%27s-Guide)
- [ ] Documentation and comments have been updated  => N/A
- [ ] `devtools::document()` has been run   => No, because that updates irrelevant files
- [x] `devtools::check()` passes with no errors or warnings
- [x] Test case demonstrating new functionality is included
- [x] Maintainers are allowed to edit this PR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc3d33ae9859`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.