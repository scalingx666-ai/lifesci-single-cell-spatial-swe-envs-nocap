# Issue

**Title:** Allow `split.adjust = list(scales = "free")` to work as intended

## Description

PR utilizes knowledge that I did not have when originally writing code for most `min` / `max` inputs -- that you can give `limits = c(<some_min>, NA)` or `c(NA, <some_max>)` to have ggplot fill in the NA side, at plot time, based on the min/max of the plot's/facet's data--both to simplify these code chunks & to allow better control of faceting by letting `split.adjust` work as intended, re: #114 

For example, `split.adjust = list(scales = "free")` could now be used in dittoPlot() to let facets zoom in on their own data:
```
library(dittoSeq)
example(importDittoBulk, echo = FALSE)
# without 'split.adjust'
dittoPlot(object = myRNA, var = dittoSeq:::.extract_Reduced_Dim("tsne", 1, myRNA)$embeddings, group.by = "timepoint",
    split.by = c("clustering"))
```
![image](https://user-images.githubusercontent.com/38870347/182449301-2c85d9e1-a6ef-4383-ba97-b8ae36a1a844.png)

```
# with 'split.adjust'
dittoPlot(object = myRNA, var = dittoSeq:::.extract_Reduced_Dim("tsne", 1, myRNA)$embeddings, group.by = "timepoint",
    split.by = c("clustering"),
    split.adjust = list(scales = "free"))
```
![image](https://user-images.githubusercontent.com/38870347/182449413-5c0c4d40-a0df-4b69-b14a-0bbe3a29b4e0.png)

ToDo:
- [x] Test a bit more extensively.
- [x] Check for stale documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0a2946c76f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.