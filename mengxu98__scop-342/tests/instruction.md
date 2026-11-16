# Issue

**Title:** fix: harden CHOIR and Cell2fate runtime safety

## Description

## Summary

- harden the optional CHOIR backend with pinned-commit namespace verification, safe overwrite semantics, complete-result validation, platform checks, and a telemetry-free isolated source install path
- harden Cell2fate result ownership, Seurat metadata ownership, external locking, symlink handling, cache fingerprints, strict posterior schemas, artifact hashes, and crash-safe staged publication
- add bounded runner diagnostics plus atomic JSON/lock helpers and focused regression coverage

## Validation

- `test-runner-utils.R`: 14/14 expectations passed
- `test-choir.R`: 104/104 expectations passed
- `test-cell2fate.R`: 76/76 expectations passed
- unchanged `test-cell2location.R` at the exact commit: 45/45 expectations passed
- `test-prepare-env-external-wrappers.R`: 21/21 expectations passed
- real CHOIR run on 60 `pancreas_sub` cells completed with pinned commit `e9ebfbc9089beeaf4ca088c7b81b18f39758b0bc`; fresh temporary-library install also passed
- real Cell2fate run on 80 `pancreas_sub` cells and 50 genes completed for 2 modules / 1 epoch; direct returned-object resume reused the result, removed a stale staging directory, and passed artifact integrity checks
- a brand-new Python 3.9 Cell2fate environment installed and imported `cell2fate 0.1a0`, `setuptools 80.9.0`, and `jaxlib 0.4.10` at commit `c03d1ca0bb963f550001c6070d4986a61ec8456a`
- `_R_CHECK_FORCE_SUGGESTS_=false R CMD check --no-manual --as-cran --no-examples --no-tests`: 0 errors, 2 existing warnings, 4 existing notes; `dependencies in R code` and `unstated dependencies in examples` are both OK

## Remaining scope

- CPU execution and small real-data smoke paths were validated; GPU execution, large production datasets, and biological-quality benchmarking remain outside this focused wrapper-safety PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d60d8a76aad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.