# Issue

**Title:** Add official SpaTalk CCC backend

## Description

## Stack

Depends on #350. This branch is based on the PR 1 commit; once #350 merges, GitHub will show only the SpaTalk layer here.

## What changed

- Added `RunSpaTalk()` using the official `ZJUFanLab/SpaTalk` R backend and `SpaTalkPlot()` for stored network, bubble, pathway, and receptor-TF results.
- Added optional-backend helpers that preflight with `check_r()` and resolve every SpaTalk function with `get_namespace_fun()`.
- Added strict raw-coordinate and explicit-image handling, single-cell and spot-plus-reference NNLM modes, named results, minimal/full native-object storage, and unified CCC output.
- Added the official SpaTalk and NNLM repositories only to `Remotes`; they were not added to Imports, Depends, or Suggests.
- Kept SpaTalk out of the `RunCCC()` defaults and did not restore a public spatial registry/schema API.

## Validation

- SpaTalk focused tests: 69 expectations passed, including single image, multi-image rejection, ID ordering, atomic failure, storage modes, explicit `RunCCC()` dispatch, and multi-result plot selection.
- Official SpaTalk 1.0 live run on a 55-cell/996-gene STARmap subset completed with 17 interactions; stored LR rows and native p-values matched the official object.
- `RunSpaTalk.Rd` and `SpaTalkPlot.Rd` were regenerated and parsed.
- Completed-stack `R CMD check` reported `checking dependencies in R code ... OK` and `checking for unstated dependencies in examples ... OK`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8336064d1190`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.