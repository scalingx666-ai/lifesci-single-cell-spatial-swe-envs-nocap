# Issue

**Title:** Xenium support

## Description

Preliminary Xenium support for Seurat. Opening this as a draft to get the discussion going. We are very open to suggestions about how to approach this.  I'm also curious what general work in required in the `feat/imaging` branch before it can merge to `develop`. We should have some bandwidth to help with that.

Open questions:
- [x] `transcripts.csv.gz` loading speed - this seems to be the bottleneck for most datasets.  We currently use `read.csv`, but could we try `readr::read_csv` or `data.table::fread`? 
- [x] `transcripts.csv.gz` - probably want to make optional? Can get very large.
- [x]  How to handle "Negative Control Probe" and "Negative Control Padlock" feature types. These are encoded as a separate `feature_type` in the matrix, but they are really technical controls of the in-situ RNA assay. They aren't useful for biological analysis, but we emit them to help users assess the specificity of the assay. Right now we're just dropping them in `LoadXenium` - should we provide an optional way to include them?
- [ ] Morphology image - do we want to have the DAPI image available as a background, similar to how we have the H&E image for Visium.
- [x] refine version requirements: I don't think SeuratObject 4.1.1 is actually required. It's possible the sp 1.5 is required, but that version is specified in SeuratObject.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b23ae2e3b0bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.