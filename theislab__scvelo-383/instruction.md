# Issue

**Title:** Improve developer installation and guide

## Description

## Changes

* Packages used in the codebase but missing in `requirements-dev.txt` are added to the file.
* The `dev` installation option in `setup.py` is refactored to collect the required packages from `requirements-dev.txt`.

## New

* `CONTRIBUTING.md` is added as a contribution guide.

## Related issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed7aa5cbd5d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.