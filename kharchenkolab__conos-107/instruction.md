# Issue

**Title:** Fix parseCellGroups() to check if clustering exists

## Description

Motivated by the following issue: 

It looks like there's a flaw in the logic of `parseCellGroups()`, which resulted in an error thrown, e.g. 

```
> con$plotPanel(font.size=4)
> con$plotPanel(font.size=4, clustering="multilevel")
Error in getClusteringGroups(self$clusters, clustering) : 
  clustering multilevel hasn't been calculated
```
  
These changes fix this behavior by checking if the `clustering` given exists. If not, throw an informative error. 

Following the walkthrough
https://github.com/kharchenkolab/conos/blob/master/doc/walkthrough.md

```
> plotComponentVariance(con, space='PCA')
> con$plotPanel(clustering="multilevel", use.local.clusters=TRUE, title.size=6)
> con$findCommunities(method=leiden.community, resolution=1)
> con$plotPanel(font.size=4)
> plotClusterBarplots(con, legend.height = 0.1)
> plotClusterBarplots(con, legend.height = 0.1, clustering="leiden")
> plotClusterBarplots(con, legend.height = 0.1, clustering="walktrap")
Error in parseCellGroups(conos.obj, clustering, groups) : 
  Clustering walktrap does not exist, run findCommunity() first
```

This behavior is expected, as `"walktrap"` clustering was never performed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec4502e87835`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.