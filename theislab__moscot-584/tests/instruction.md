# Issue

**Title:** [pre-commit.ci] pre-commit autoupdate

## Description

<!--pre-commit.ci start-->
updates:
- [github.com/psf/black: 23.3.0 → 23.7.0](https://github.com/psf/black/compare/23.3.0...23.7.0)
- https://github.com/timothycrosley/isort → https://github.com/PyCQA/isort
- https://github.com/charliermarsh/ruff-pre-commit → https://github.com/astral-sh/ruff-pre-commit
- [github.com/astral-sh/ruff-pre-commit: v0.0.277 → v0.0.278](https://github.com/astral-sh/ruff-pre-commit/compare/v0.0.277...v0.0.278)
<!--pre-commit.ci end-->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f117d610b68`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.