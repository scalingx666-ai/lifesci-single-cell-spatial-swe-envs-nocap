# Issue

**Title:** Bugfix: add check if el is empty

## Description

I think this will address 

Basically, there needs to be a check if `el` is empty here: https://github.com/kharchenkolab/conos/blob/master/R/conclass.R#L183

```
## Merge the results into a edge table
el <- do.call(rbind, mnnres)
```

If so, make `el` an empty dataframe with correct columns, and the downstream functions work as expected. 

This works for me:
```
library(conos)
library(dplyr)
library(pagoda2)

panel.preprocessed <- readRDS(".../seurat_list.Rds") ### https://we.tl/t-7nBieo9xKX

con <- Conos$new(panel.preprocessed, n.cores=4)

con$buildGraph(space="genes")

print(con$graph)
## IGRAPH ead3ad7 UNW- 2000 13642 -- 
## + attr: name (v/c), weight (e/n), type (e/n)
## + edges from ead3ad7 (vertex names):
##  [1] Cell66 --Cell1   Cell66 --Cell353 Cell66 --Cell300 Cell66 --Cell365
##  [5] Cell66 --Cell367 Cell66 --Cell139 Cell66 --Cell309 Cell66 --Cell362
##  [9] Cell66 --Cell106 Cell66 --Cell100 Cell1  --Cell135 Cell1  --Cell230
## [13] Cell1  --Cell248 Cell1  --Cell253 Cell1  --Cell349 Cell1  --Cell353
## [17] Cell1  --Cell397 Cell1  --Cell443 Cell1  --Cell467 Cell135--Cell349
## [21] Cell135--Cell397 Cell135--Cell239 Cell135--Cell425 Cell135--Cell422
## [25] Cell135--Cell400 Cell135--Cell410 Cell135--Cell309 Cell135--Cell354
## [29] Cell135--Cell459 Cell135--Cell64  Cell135--Cell102 Cell135--Cell245
## + ... omitted several edges

```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a5eceaec6cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.