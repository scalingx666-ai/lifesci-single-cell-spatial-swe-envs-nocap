# Issue

**Title:** Fix for #10074 providing multiple resolutions to `FindClusters`

## Description

Hi Seurat Team,

This is quick fix for issue #10074.  Changes in the 5.3.1 dev branch resulted in error when providing multiple resolutions to `FindClusters`.  Just a simple swap to account for number of names being length greater than 1:

```
if (cluster.name == default.cluster.name)
```
for
```
if (isTRUE(x = all(cluster.name %in% default.cluster.name)))
```

Thanks as always!
Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5d9535493fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.