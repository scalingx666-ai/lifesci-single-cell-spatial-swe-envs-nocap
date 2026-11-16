# Issue

**Title:** Fix factor level ordering for FindClusters columns

## Description

# Errors
The following errors have been reported at:

- 

## Error 1

When running FindClusters(), the active identities and seurat_clusters are re leveled into numeric order, but the resolution specific metadata columns, for example RNA_snn_res.3, can retain lexicographically ordered factor levels:

```{R}
pbmc_small <- FindClusters(pbmc_small, resolution = 3, verbose = FALSE)

table(pbmc_small$seurat_clusters)
table(pbmc_small$RNA_snn_res.3)
```

```{R}
> table(pbmc_small$seurat_clusters)

 0  1  2  3  4  5  6  7  8  9 10 
14 12 10  9  9  5  4  7  3  5  2 

> table(pbmc_small$RNA_snn_res.3)

 0  1 10  2  3  4  5  6  7  8  9 
14 12  2 10  9  9  5  4  7  3  5 
```

FindClusters.Seurat currently assigns the resolution columns into object metadata via:
```{R}
object[[]] <- clustering.results
```
After metadata assignment, FindClusters.Seurat relevels Idents(object) into numeric order and copies the corrected factor into seurat_clusters or cluster.name. This change normalizes factor levels for all clustering result columns after they are renamed to their final metadata column names and before they are written into the object. Numeric looking levels are ordered numerically, and any non numeric levels are appended after the numeric set.

This previous pull request () fixed lexicographic ordering for custom cluster.name by ensuring the corrected Idents(object) factor was used, but it did not modify any already written metadata columns, resulting in this lingering issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `334545e8ab85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.