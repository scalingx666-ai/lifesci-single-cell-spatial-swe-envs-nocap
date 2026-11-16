# Issue

**Title:** Switch to pytest importlib import mode

## Description

Switch to pytest's `importlib` import mode, the recommended setting for `src`-layout packages.

## Why

The default `prepend` mode puts `tests/` on `sys.path`, which:
- Pollutes the module namespace (test helpers importable as top-level modules)
- Undermines the `src` layout (meant to isolate installed package from source tree)
- Can cause name collisions if test files shadow real package modules

`importlib` mode loads test files via `importlib.import_module()` without modifying `sys.path`, catching real import bugs that `prepend` hides.

## Changes

- Add `tests/__init__.py` (empty) — makes `tests` a proper package
- Change `from _helpers import ...` → `from tests._helpers import ...` in all 7 test files
- Add `addopts = ["--import-mode=importlib"]` to `[tool.pytest.ini_options]`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a1d4fe95ebb5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.