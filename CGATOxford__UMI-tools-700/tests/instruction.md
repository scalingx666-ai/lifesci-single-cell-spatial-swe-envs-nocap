# Issue

**Title:** fix: rename build backend module to use underscore instead of hyphen

## Description

## Problem

The hyphen in `setuptools-cython` is an invalid Python identifier.
Tools like `uv` and `pixi` generate an import statement at build time that causes a hard SyntaxError:

```
      [stderr]
        File "<string>", line 8
          import setuptools-cython as backend
                           ^
      SyntaxError: invalid syntax
```

## Fix

- Renamed `setuptools-cython/setuptools-cython.py` to `setuptools_cython.py`
- Updated `build-backend` in `pyproject.toml` from `"setuptools-cython"` to `"setuptools_cython"`

The `backend-path` pointing to the `setuptools-cython/` directory is unchanged.

## Tested

Confirmed the SyntaxError reproduces in a clean venv before the fix, and
that `uv pip install .` succeeds after.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f109b2adc53e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.