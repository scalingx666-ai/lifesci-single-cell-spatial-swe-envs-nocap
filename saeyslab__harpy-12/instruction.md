# Issue

**Title:** SC_5 subset adata

## Description

implementation of  see https://github.com/saeyslab/harpy/blob/2f3e8f012460c8d573ae4ad0e161138ad96a7cac/src/sparrow/_tests/test_table/test_clustering.py#L18 for usage. 

Currently opted to subset the adata, and removing the channels that are not selected for clustering. 

I do not feel comfortable with the alternative: "adding this as an annotation like a boolean mask "lineage" in the AnnData.var ",  because for a user it not clear any more from the anndata where the e.g. leiden clusters, neighbours,... where calculated on.
If user is interested in keeping all channels, the resulting table after clustering could be saved in a different table slot of the SpatialData object.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96dfab051c29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.