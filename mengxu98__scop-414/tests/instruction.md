# Issue

**Title:** fix(ci): install `geometry` for the giotto optional suite

## Description

## Problem

After #413, the giotto suite of `optional-backends` still fails (run [34355614606](https://github.com/mengxu98/scop/actions/runs/34355614606)):

```
── 1. Error ('test-framework-bridges.R:235:3'): srt_to_giotto and giotto_to_srt …
Error: package 'geometry' is not yet installed
```

`GiottoClass::seuratToGiottoV5()` estimates Visium scale factors through a Delaunay network built by `createNetwork(type = "delaunay", method = "geometry")`, and `geometry` is a *Suggests* of GiottoClass, so pak does not install it with the suite.

## Fix

- Install `cran::geometry` for the giotto suite (and verify it through `required`).
- `skip_if_not_installed("geometry")` in the live round-trip, so the test degrades instead of erroring in environments without the optional package.

## Validation

- `testthat::test_local(filter = "framework-bridges")` — 36 tests pass locally (GiottoClass + geometry installed).
- Workflow YAML parses; the giotto matrix entry now lists `cran::geometry`.
- `optional-backends` will be re-dispatched on `main` after merge to confirm the suite turns green.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e908811b435b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.