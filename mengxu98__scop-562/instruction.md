# Issue

**Title:** fix: stop PrepareEnv from installing conflicting pandas pins

## Description

## Problem

A default `PrepareEnv()` fails with:

```
ERROR: Cannot install pandas==2.0.3 and pandas==2.2.0 because these package versions have conflicting dependencies.
```

This is not a user-side conda problem. It reproduces on `main` with the default module set (the reported log contains `SEACells` and `joblib`, both default modules).

## Root cause

1. `core_python_requirements()` pins `pandas==2.2.0`; `magic`/`phate` pin `pandas==2.0.3` for the isolated `scprep_env`; `tage`/`scfea` add an unpinned `pandas`.
2. `env_requirements()` concatenates module specs with `c()`. Named `[<-` only replaces the first duplicate, so several entries named `pandas` survive in the requirement vector.
3. `resolve_requested_python_packages()` builds its lookup with `normalize_env_modules(include_optional = TRUE)`, which contains `magic`. The unpinned `pandas` is therefore resolved to `2.0.3`, while the explicit `2.2.0` pin is kept as-is.
4. `unique_python_requirements()` deduplicates by string value, so both pins reach pip in the same command.

## Changes

- `R/PrepareEnv.R`: emit one pin per package before returning and realign `install_methods` (they are matched to packages by position); inline the optional module list without `magic` and `moscot`, so the `optional` shortcut no longer drags the default stack into `scprep_env` or mixes incompatible JAX profiles.
- `R/check_packages.R`: exclude isolated profiles from the shared version lookup while retaining their exclusive package pins (`magic-impute==3.0.0`, `phate==1.0.11`, ...); deduplicate requirements by canonical distribution name, prefer explicit pins and warn when genuinely conflicting pins are requested.
- `NEWS.md`: record the fix.
- Regression tests covering one-pin-per-package / method alignment, the default install, isolated profile lookups, the `optional` shortcut, and conflict warnings.

The deliberate guard for explicitly requesting `scvi` together with `moscot` is unchanged; those modules still need separate environments.

## Verification

- `testthat::test_local()` over the python/env related test files: 1200 assertions, 0 failures, 0 errors (only pre-existing `ddiMatrix` coercion warnings and platform skips).
- Reverting the fix makes 6 of the new regression tests fail (15 assertions, 0 skips), so the tests genuinely cover the reported conflict rather than passing vacuously.
- Repro script: the default full install now passes a single `pandas==2.2.0` to pip, with `SEACells` / `joblib` still present; an explicit `scvelo + magic` request still yields `pandas==2.0.3` in `scprep_env`.
- `resolve("pandas") = pandas==2.2.0`, `resolve("magic-impute") = magic-impute==3.0.0`, `resolve("phate") = phate==1.0.11`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dba12251a532`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.