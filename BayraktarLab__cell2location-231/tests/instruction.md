# Issue

**Title:** [pre-commit.ci] pre-commit autoupdate

## Description

<!--pre-commit.ci start-->
updates:
- https://github.com/python/black → https://github.com/psf/black
- [github.com/psf/black: 22.3.0 → 22.12.0](https://github.com/psf/black/compare/22.3.0...22.12.0)
- https://gitlab.com/pycqa/flake8 → https://github.com/PyCQA/flake8
- [github.com/PyCQA/flake8: 3.8.4 → 6.0.0](https://github.com/PyCQA/flake8/compare/3.8.4...6.0.0)
- [github.com/pycqa/isort: 5.7.0 → 5.11.4](https://github.com/pycqa/isort/compare/5.7.0...5.11.4)
<!--pre-commit.ci end-->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57e2d65b2ebd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.