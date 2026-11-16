# Issue

**Title:** Handle degenerate inputs to FindSpatiallyVariableFeatures

## Description

The follow-up I offered in , targeting `fix/findspvariable-fov` so it can be merged into that branch or ignored, whichever suits you.

One correction up front: I called the second finding "one word on the line just below the new guard." That was wrong. `drop = FALSE` is necessary but not sufficient, and writing the reproduction turned up two more shapes that reach the same code. Five in total, each ending in a message that says nothing about the cause.

## What breaks

| Input | Today | Cause |
|---|---|---|
| `spatial.location` with one matching row name | `argument is of length zero` | `RowVar()` divides by `ncol - 1` |
| Exactly one feature survives the variance filter | `argument is of length zero` | subset drops to a vector |
| ... with `selection.method = "markvariogram"` | `$ operator is invalid for atomic vectors` | `markvario()` returns a bare `fv` |
| `RunMarkVario()` under a parallel plan | silently wrong result | same, per chunk |
| No feature survives the variance filter | `attempt to set 'colnames' on an object with less than two dimensions` | `svf.info` is `c()` |

## The five

**1. The `!ncol(data)` guard lets a one-column matrix through.** `!any(cells %in% ...)` only needs a single match, so a `spatial.location` holding one real cell name and eleven that match nothing clears both new checks. `RowVar()` divides by `ncol - 1`, so every feature comes back `NaN`, `NaN > 0` is `NA`, and the subset degenerates before `nrow()` is reached. Widened to `ncol(data) < 2`, with a message that names the reason.

**2. `data[RowVar(data) > 0, ]` needs `drop = FALSE`.** With exactly one surviving feature it becomes a vector, `nrow()` returns NULL, and the line below raises the same `argument is of length zero`.

**3. `markvariogram` needs more than that.** `markvario()` returns a bare `fv` for a single mark and a named list of them for several. `ComputeRMetric()` iterates over its argument, so one surviving feature hit `$ operator is invalid for atomic vectors`. The single-mark case is now normalized to a list, the shape the caller already assumes.

**4. The same variable shape corrupts `RunMarkVario()` under a parallel plan, silently.** Features are split into one chunk per worker, and a chunk holding a single feature contributes its four `fv` columns to `unlist()` instead of one entry, so the names assigned afterwards run off the end:

```r
plan("multisession", workers = 2)
marks <- matrix(rnorm(36), nrow = 3, dimnames = list(paste0("g", 1:3), paste0("c", 1:12)))
RunMarkVario(spatial.location = pos, data = marks)
#> length 6, names g1, g2, g3, NA, NA, NA
```

Five features over two workers split 3 and 2, so neither chunk is size one and the result is fine, which is presumably why this went unnoticed. Each chunk is normalized the same way now, and subset with `drop = FALSE` so a one-feature chunk stays a matrix and `t()` keeps one row per cell.

**5. Nothing survives the variance filter.** `svf.info` is set to `c()` and both selection branches index into it. The empty branch reads as deliberate, so it now warns and returns the object unchanged rather than falling through.

## Scope

All five are reachable on `main`. Only the first sits downstream of the guard this branch adds; the rest are independent of your change but live in the same function, and the single-feature ones are on the path your new test exercises. Happy to split 4 out into its own PR against `main` if you would rather keep this branch tight, or drop any of it.

I did not touch the third point from my review, the "provide `spatial.location`" half of the segmentation message pointing at an argument `FindSpatiallyVariableFeatures.Seurat` does not have. That is wording on your new code, so it seemed yours to decide.

Nor did I add a test for 4: nothing in `tests/testthat` currently sets a `future` plan, and introducing `multisession` there is a convention change plus a CI cost. There is a direct shape test for `RunMarkVario` with one feature instead, which covers the sequential half. The reproduction above is there if you would rather have the parallel case tested.

## Tests

Four new blocks in `test_spatial.R`: the two-cell minimum, a single varying feature under both selection methods, the warn-and-return path under both, and `RunMarkVario` shape for one and three features. Each fails on this branch without the corresponding fix.

Full suite with `NOT_CRAN=true`, R 4.6.1, macOS arm64: 17 files, 1209 expectations, 0 failures.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ebc3b786181`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.