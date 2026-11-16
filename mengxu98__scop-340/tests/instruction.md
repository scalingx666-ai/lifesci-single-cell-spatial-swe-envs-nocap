# Issue

**Title:** fix: harden CHOIR and Cell2fate runtime boundaries

## Description

## Summary

Follow-up hardening after merged PRs #335 and #336, rebased onto current `main` after #341.

- reject numeric `max_clusters` before CHOIR backend execution because the pinned upstream full-tree loop can fail to terminate when cluster counts plateau; keep the tested `auto` path unchanged
- reserve Python 3.9 for the standalone Cell2fate environment
- treat malformed Cell2fate resume manifests as cache misses, allowing safe recovery with `overwrite = TRUE`
- preserve character IDs such as `001`, `010`, and literal `NA` when reading runner CSV output
- retain Python stderr independently even when stdout is long
- reuse one internal runner implementation across Cell2fate and Cell2location for script discovery, JSON I/O, scoped environment variables, CSV parsing, numeric validation, and failure diagnostics
- remove Cell2location plotting tests; no test plots or image artifacts are generated or uploaded
- keep both backends optional: no DESCRIPTION, NAMESPACE, hard-dependency, global-option, or persistent environment-variable changes

## Simplification

The unification commit changes 6 files by `+255/-324` (net -69 lines). Across the complete PR, 11 files are `+423/-260`; most additions are real behavior tests rather than duplicated runtime code.

## Validation

After the rebase and unification:

- all 8 changed R/test files parse successfully
- `git diff --check origin/main...HEAD` passes
- `test-cell2fate.R`: 50 passed, 0 failed; one Python-version probe skipped on this Windows host
- `test-cell2location.R`: 45 passed, 0 failed
- standalone CHOIR `auto`/numeric validation contract passed
- full local CHOIR execution could not be repeated with `compile = FALSE` because the package's native DLL is intentionally unavailable in that mode; GitHub R-CMD-check and coverage perform the authoritative full build

Original real `pancreas_sub` smoke validation from this PR remains applicable:

- CHOIR: 60 real cells, `max_clusters = auto`, CPU, completed twice; no missing final labels; provenance records upstream commit `e9ebfbc9089beeaf4ca088c7b81b18f39758b0bc`
- Cell2fate: 80 real cells, 50 input genes / 46 retained genes, CPU, one training epoch, 80/80 posterior rows mapped back; provenance records upstream commit `c03d1ca0bb963f550001c6070d4986a61ec8456a`
- repeated Cell2fate run reused the matching result
- a deliberately corrupted manifest with `resume = TRUE, overwrite = TRUE` caused a real retrain and produced a new complete manifest

## Scope boundary

These runs validate wrapper integration, error handling, cache recovery, and small CPU execution. They do not claim GPU, production-scale, long-training, or biological-performance validation.
## Final CI

- R-CMD-check passed on macOS, Ubuntu, and Windows
- pkgdown passed
- coverage passed with `FAIL 0 | WARN 21 | SKIP 26 | PASS 3052`
- the real isolated benchmark error path passed locally in 23.38 seconds and under covr after raising its startup allowance from 30 to 120 seconds
- no plotting tests or image artifacts were added by this PR

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85b076669d16`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.