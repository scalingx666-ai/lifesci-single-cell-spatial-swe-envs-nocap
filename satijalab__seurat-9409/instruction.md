# Issue

**Title:** Fix ggplot2 deprecation warning in DotPlot()

## Description

# Problem

The `facets` argument of `facet_grid()` is deprecated as of ggplot2 2.2.0. And aes_string() is deprecated as of ggplot2 3.0.0. The warnings are disturbing and will be errors in the future.

# Fix

1. Use `rows`  argument for `facet_grid()`.
2. Switch `aes_string()` to `aes()` and use tidy evaluation idioms.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24601d1b1b93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.