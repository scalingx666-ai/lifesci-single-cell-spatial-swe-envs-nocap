# Issue

**Title:** Ask for as many components as the data has

## Description

`SketchData()` fails on any small object, at every size of sketch:

```r
> SketchData(pbmc_small, ncells = 40, method = "LeverageScore")
Error: max(nu, nv) must be strictly less than min(nrow(A), ncol(A))
```

## Cause

`LeverageScore.default()` sizes its decomposition to the object, and then does not use the value:

```r
nv <- ifelse(nrow(x = object) < 50, nrow(x = object) - 1, 50)
...
Z <- irlba(A = object, nv = 50, nu = 0, verbose = FALSE)$v
```

`nv` is computed and dropped; 50 components are always requested. Anything with fewer than 50 features or cells on the side being decomposed therefore stops inside `irlba`, and since `SketchData()` is how `LeverageScore()` is usually reached, that is where it surfaces.

## Fix

Use `nv`, bounded by both dimensions, and say so when there is nothing to decompose at all:

```
Cannot compute leverage scores from 1 features and 1 cells: at least two of each are needed
```

Behaviour is unchanged for objects with 50 or more of each, which is where the constant and the computed value agree.

## Tests

`tests/testthat/test_leverage_score_small.R`: leverage scores on `pbmc_small`, sketching to 40 cells, asking for more cells than exist (all of them are kept), and the message for a matrix with nothing to decompose.

Four assertions fail without the change. Full suite `NOT_CRAN=true`: 1187 passing, the only 2 failures being the pre-existing `Read10X_Image` ones fixed in #10454.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f67c701ecc6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.