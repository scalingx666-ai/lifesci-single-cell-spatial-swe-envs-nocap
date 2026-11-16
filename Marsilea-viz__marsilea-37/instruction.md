# Issue

**Title:** Enable the specified precomputed chunk linkage.

## Description

Use case: When analyzing single-cell data, we may sometimes need to calculate the cluster linkage based on the PC results and then use that linkage for other analyses, such as identifying spec genes.


```

h.add_dendrogram(
    'top', add_base=False, meta_linkage=adata.uns['dendrogram_Cluster']['linkage']
)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b7562274317`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.