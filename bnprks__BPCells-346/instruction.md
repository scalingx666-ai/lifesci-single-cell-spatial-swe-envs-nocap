# Issue

**Title:** [r] Fix `c()` of a single fragments object

## Description

## Context

Part of #344 (proposed PR 2). `c()` of a single fragments object returns a one-element list instead of the object, because `return(fragments_list)[[1]]` returns before it indexes:

```r
frags <- GenomicRanges::GRanges("chr1", IRanges::IRanges(c(1, 100), width = 50), cell_id = c("a", "b")) |>
  convert_to_fragments() |>
  write_fragments_memory()
class(c(frags))
#> [1] "list"
```

Code that combines a variable number of samples, such as `do.call(c, fragments_by_sample)`, then fails when there is only one sample.

## Changes

- Index the list before returning it: `return(fragments_list[[1]])`.
- Add a regression test for `c(frags)` and `do.call(c, list(frags))`.
- Add a NEWS entry.

## Testing

Full test suite, every file in `tests/testthat` with `testthat::test_file()` (R 4.5.3, Linux): 146 tests and 2,868 expectations, no failures. The new test fails on `main`, where `c(frags)` returns a list.

## Disclosure

Claude Code was used to help investigate the issue and draft this PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `016296413cd7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.