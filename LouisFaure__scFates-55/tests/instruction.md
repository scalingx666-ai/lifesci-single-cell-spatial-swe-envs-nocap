# Issue

**Title:** Refactor to pyproject.toml and add pixi support

## Description

Refactored the project to use `pyproject.toml` for configuration and dependency management, replacing `setup.py` and `requirements.txt`. Removed a duplicate `adjustText` dependency. Introduced `pixi` for setting up the development environment, which simplifies handling R dependencies. Updated `README.md` with instructions on using `pixi` and added release notes for version 1.2.1. Verified that tests pass in the `pixi` environment.

---
*PR created automatically by Jules for task [1843137479045884862](https://jules.google.com/task/1843137479045884862) started by @LouisFaure*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35674454ba38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.