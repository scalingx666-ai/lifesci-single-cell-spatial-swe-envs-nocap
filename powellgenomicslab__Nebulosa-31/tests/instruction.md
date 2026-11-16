# Issue

**Title:** add missing imports

## Description

@joseah `SeuratObject` is listed in NAMESPACE, but is missing in DESCRIPTION.

This goes as far as failed installation of `SeuratWrappers`, which has `Nebulosa` as a remote dependencies, which should misses `SeuratObject`. This became especially clear when using NixPkgs for reproducible environments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1f0714dd4ade`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.