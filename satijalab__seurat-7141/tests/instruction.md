# Issue

**Title:** spaceranger 2.1 update

## Description

This pull request makes updates to 
`Load10X_Spatial` and `Read10X_h5` to accommodate the new output of spaceranger 2.1 (which is still in development)

This PR

- Allows for the new `raw_probe_bc_matrix.h5` to be loaded by `Load10X_Spatial`
  - This file contains individual probe level counts and information 
- Adds probe meta-data to the Spatial assay of the seurat object
- New function called `Read10x_probe_metadata`

The structure of the `raw_probe_bc_matrix.h5` is as follows
```
/matrix                  Group
/matrix/barcodes         Dataset {4987}
/matrix/data             Dataset {17581240/Inf}
/matrix/features         Group
/matrix/features/feature_type Dataset {21178}
/matrix/features/filtered_probes Dataset {21178}
/matrix/features/gene_id Dataset {21178}
/matrix/features/gene_name Dataset {21178}
/matrix/features/genome  Dataset {21178}
/matrix/features/id      Dataset {21178}
/matrix/features/name    Dataset {21178}
/matrix/features/probe_region Dataset {21178}
/matrix/features/target_sets Group
/matrix/features/target_sets/Visium\ Mouse\ Transcriptome\ Probe\ Set Dataset {19779}
/matrix/filtered_barcodes Dataset {4987}
/matrix/indices          Dataset {17581240/Inf}
/matrix/indptr           Dataset {4988}
/matrix/shape            Dataset {2}
```

I added an example `raw_probe_barcode_matrix.h5` to the visium test folder

This will probably require a fresh `roxygenize` but I don't know your workflow and didn't want to overstep

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da62e8a5fb93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.