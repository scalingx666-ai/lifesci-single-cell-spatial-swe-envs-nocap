# Issue

**Title:** fix: restore renv across Unix CI

## Description

## Summary
- force Linux package compilation to end with C++17 so legacy packages cannot downgrade the locked RcppArmadillo toolchain to C++11
- bootstrap the exact locked RcppParallel source into an isolated Unix renv library, then reuse that library for the full restore
- on macOS, bootstrap the exact locked cli/sessioninfo sources and disable only sessioninfo's crashing external-software diagnostic before the standard restore
- install pinned CI tooling in a temporary empty renv project so it cannot accidentally resolve the package's GitHub Remotes

## Root cause
- Ubuntu restored miloR with a package-level `-std=gnu++11` flag after renv had selected RcppArmadillo 15.4.2-1, which requires C++14 or newer
- clean Unix restores scheduled RcppParallel into a dependency cycle involving Seurat/thisplot; package-subset and package-install APIs still inherited the active scop dependency graph, so the root package is installed directly from the lockfile repository before standard restore
- OmnipathR calls sessioninfo's external probe from `.onLoad()`; GitHub's arm64 macOS R runtime segfaults inside `libcurlVersion()`. R CMD INSTALL suppresses user and site startup profiles for its isolated load test, so the CI library uses the exact locked sessioninfo 1.2.3 source with only `external_info()` replaced by an empty diagnostic result
- external `rcmdcheck`/`xopen` installation inherited the active scop project and attempted to resolve unrelated `DESCRIPTION` Remotes; the shared action now passes an isolated project explicitly and supplies the workflow GitHub token

## Validation
- parsed the composite action YAML and all embedded R blocks successfully
- `git diff --check` passes
- executed the RcppParallel bootstrap locally against a temporary runner environment: downloaded and built locked RcppParallel 6.1.0 with C++17, verified it was the only project-library package, and verified the persisted `RENV_PATHS_LIBRARY` value
- the macOS bootstrap verifies exact cli/sessioninfo versions after source install and loads the patched `sessioninfo::external_info()` before continuing
- a separate compiler probe with a simulated package `-std=gnu++11` flag ended in `-std=gnu++17` and compiled successfully
- actionlint 1.7.12 only reports the repository's existing `concurrency.queue: max` syntax; real GitHub runs accept it and require it to serialize the shared renv cache jobs

No plotting tests or image artifacts were run or generated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `718a06d1dd11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.