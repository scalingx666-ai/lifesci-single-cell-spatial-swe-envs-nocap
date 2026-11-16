# Issue

**Title:** Refactor private CCC method specifications

## Description

## What changed

- Centralized CCC runner, alias, spatial, and preflight metadata in one package-private method specification.
- Kept the existing seven CCC methods, defaults, failure recording, unified bundle updates, and plotting behavior unchanged.
- Routed available-method detection and dispatch through the private specification without adding a public registry or status API.

## Why

SpaTalk and COMMOT need a small internal extension point, while current `main` intentionally removed the former public spatial registry/schema layer. This refactor creates only the minimum private dispatch surface needed for later producer PRs.

## Validation

- Existing CCC platform regression suite: 109 expectations passed; one pre-existing CellPhoneDB/LIANA evidence warning is expected.
- `pkgload::load_all('.', quiet = TRUE, compile = FALSE)` passed on the completed stack.
- Completed-stack `R CMD check` reported `checking dependencies in R code ... OK` and `checking for unstated dependencies in examples ... OK`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8336064d1190`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.