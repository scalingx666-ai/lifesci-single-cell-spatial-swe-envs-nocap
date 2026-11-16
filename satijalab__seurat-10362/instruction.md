# Issue

**Title:** Update `HTODemux` to handle HTO assays containing a subset of cells

## Description

This PR makes updates to HTO demux so in functions in the case where the HTO assay cells are a subset of the cells in the RNA assay.  This incorporates two changes as suggested in  which previously did not work with an outdated version of AverageExpression. This PR removes both instances of sorting HTO cells relative to the cell names of the complete object rather than just the first instance. As mentioned in this thread ( and ) I think part of the problem with this PR earlier was a lack of appropriate testing data.  Attached is the test that I edited based on David's initial code, but would be good to add some more testing. 

```r
# Test case for HTODemux when the HTO assay is a subset of the RNA assay

library(Seurat)

umi_raw <- readRDS("/brahms/shared/vignette-data/pbmc_umi_mtx.rds")
hto_raw <- readRDS("/brahms/shared/vignette-data/pbmc_hto_mtx.rds")

# Convert into sparse matrices
umi_counts <- as.sparse(umi_raw)
hto_counts <- as.sparse(hto_raw)

# Get the common cells from these two
common_cells <- intersect(colnames(umi_counts), colnames(hto_counts))
object_cells <- common_cells[1:1000]
hto_cells <- common_cells[1:500]

# Confirm that the HTO cells are a subset of the object cells
length(intersect(object_cells, hto_cells))

umi_counts_sub <- umi_counts[, object_cells]
hto_counts_sub <- hto_counts[, hto_cells]

# Make a Seurat object where counts come from 1000 cells
test_case <- CreateSeuratObject(counts = umi_counts_sub)

# Add the HTO assay, which is a subset of the cells from the entire dataset
test_case[["HTO"]] <- CreateAssayObject(counts = hto_counts_sub)

# Confirm that HTO cells are a subset of the object cells
all(colnames(test_case[["HTO"]]) %in% colnames(test_case))
length(setdiff(colnames(test_case), colnames(test_case[["HTO"]])))
head(setdiff(colnames(test_case), colnames(test_case[["HTO"]])))

test_case <- NormalizeData(test_case, assay = "HTO", normalization.method = "CLR")
test_case <- HTODemux(test_case, assay = "HTO") # current version fails here

# Now try the updated function that removes ordering against all object cells
test_case <- HTODemux_updated(test_case, assay = "HTO") # this works

# Confirm that the updated version also works when all cells are included
no_subset_object <- CreateSeuratObject(counts = umi_counts)
no_subset_object[["HTO"]] <- CreateAssayObject(counts = hto_counts)

no_subset_object <- NormalizeData(no_subset_object, assay = "HTO", normalization.method = "CLR")
no_subset_object <- HTODemux(no_subset_object, assay = "HTO")
no_subset_object <- HTODemux_updated(no_subset_object, assay = "HTO")

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `387425908a9b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.