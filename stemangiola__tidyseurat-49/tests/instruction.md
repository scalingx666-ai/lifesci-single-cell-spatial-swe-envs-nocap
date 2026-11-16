# Issue

**Title:** Change `pivot_longer()` argument defaults from `list()` to `NULL`

## Description

In tidyr 1.2.0 we updated `pivot_longer()`'s `names_transform`, `values_transform`, `names_ptypes` and `values_ptypes` arguments to allow a _single_ function or ptype which will be applied to all columns, rather than requiring a named list. See https://github.com/tidyverse/tidyr/blob/main/NEWS.md#pivoting

This required us to change the default argument from `list()` to `NULL`. In particular, for `names/values_ptypes`, this was important because `list()` should now be interpreted as "use a list ptype for all columns".

For backwards compatibility with tidyseurat and a few other packages that extend `pivot_longer()`, we have temporarily forced `list()` to be interpreted as `NULL`, but we would like to remove this behavior. See 

This PR is a step towards that by updating the signature used in tidyseurat to use `NULL` rather than `list()`. We would appreciate if you could merge this in and get it on CRAN at your earliest convenience!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e016c2870f03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.