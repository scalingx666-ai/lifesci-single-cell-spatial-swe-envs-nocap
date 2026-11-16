# Issue

**Title:** Fix pandas 2 error with lineage tree loading

## Description

Hi @michalk8, this is one way of fixing an error that occurred to me when trying to read in the C. elegans lineage trees via `adata, tree = moscot.datasets.c_elegans()`, see  

The problem was that node information was stored in DataFrames, which somehow caused a problem in pandas 2. I now convert dataframes to dict and save the tree in `gml` format. 

Ideally, the tree would also be cached, just like the AnnData object, but this might be fine for now?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a430200c0ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.