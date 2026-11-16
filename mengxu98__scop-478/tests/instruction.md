# Issue

**Title:** docs: clarify optional backend checks and exclude guide from builds

## Description

## Summary

- Keep `CONTRIBUTING.md` at the repository root and exclude it from R source packages with `^CONTRIBUTING[.]md$` in `.Rbuildignore`.
- Describe runtime-optional backends separately from the current `Remotes` entries (`thisplot` and `thisutils`, both imported helpers).
- Document that `check_r()` defaults to installation and that `verbose = FALSE` does not disable it. Require non-installing availability checks and explicit setup for examples/checks, while preserving the existing helper, logging, startup, and print conventions.

No runtime code, package dependencies, examples, or generated documentation changed.

## Validation

- Based on upstream `main` at `633c0cabc8e66eed222908a80ea58883a8e00d9f`.
- `git diff --check` passed; all relative documentation links resolve.
- Verified the installation behavior against the pinned `thisutils` source (`bb62888fbf17e5988d71012677df3c47693290b2`).
- Built the baseline and patched package with R 4.5.0 on Debian 13 using `R CMD build --no-build-vignettes --no-manual --no-resave-data`.
- Compared both tarball file lists: the baseline includes `scop/CONTRIBUTING.md`; the patched archive excludes it, and the repository file remains present.
- Ran the same focused check on both tarballs with `_R_CHECK_TOPLEVEL_FILES_=true _R_CHECK_RD_XREFS_=false _R_CHECK_FORCE_SUGGESTS_=false R CMD check --no-install --no-manual --no-vignettes --no-examples --no-tests`.
  - Baseline: `checking top-level files ... NOTE`, naming `CONTRIBUTING.md`.
  - Patched: `checking top-level files ... OK`.
  - The remaining diagnostics are identical: 3 warnings (`theme_scop` documentation mismatch, undocumented `RunSingleR` arguments, and data loading without the cloud workspace's uninstalled dependencies) and 2 notes (`LinkingTo` include directories unavailable in this minimal R environment, and existing `PKG_CFLAGS` usage).

This is focused packaging/documentation validation, not a full installed-package or backend test pass. Package installation, examples, tests, vignettes, and Rd cross-reference checks were not included in that focused run; the PR workflow provides the normal CI checks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bc67bf6026b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.