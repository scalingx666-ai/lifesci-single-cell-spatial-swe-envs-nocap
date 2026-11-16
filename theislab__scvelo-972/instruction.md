# Issue

**Title:** Move package setup to toml file

## Description

## Changes

<!-- Please remove section if this PR does change an existing feature -->

- Updates `pyproject.toml` to set up project.
- Removes `setup.py`, `requirements.txt`, `requirements-dev.txt`, `docs/requirements.txt`.
- Updates `CONTRIBUTING.rst` and `installation.rst` to remove outdated reference to `requirements-dev.txt`.

## Related issues

<!-- Please list related issues. If none exist, open one and reference it here. -->

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0cbd579fc62c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.