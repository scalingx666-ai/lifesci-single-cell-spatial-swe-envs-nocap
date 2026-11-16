# Issue

**Title:** Use initialize() method instead of prototype for Params class

## Description

This PR is intended to resolve issue #132.

Testing examples: 

``` r
set.seed(1)
obj1 <- splatter::newSplatPopParams()
splatter::getParam(obj1, "seed")
#> [1] 602245

set.seed(2)
obj2 <- splatter::newSplatPopParams()
splatter::getParam(obj2, "seed")
#> [1] 308175

set.seed(1)
obj3 <- splatter::newSplatPopParams()
splatter::getParam(obj3, "seed")
#> [1] 602245
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1eec243e946f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.