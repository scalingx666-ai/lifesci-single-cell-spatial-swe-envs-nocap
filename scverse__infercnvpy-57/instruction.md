# Issue

**Title:** [pre-commit.ci] pre-commit autoupdate

## Description

<!--pre-commit.ci start-->
updates:
- [github.com/psf/black: 22.6.0 → 22.10.0](https://github.com/psf/black/compare/22.6.0...22.10.0)
- [github.com/pre-commit/mirrors-prettier: v2.7.1 → v3.0.0-alpha.1](https://github.com/pre-commit/mirrors-prettier/compare/v2.7.1...v3.0.0-alpha.1)
- [github.com/asottile/yesqa: v1.3.0 → v1.4.0](https://github.com/asottile/yesqa/compare/v1.3.0...v1.4.0)
- https://github.com/myint/autoflake → https://github.com/PyCQA/autoflake
- [github.com/PyCQA/autoflake: v1.4 → v1.7.1](https://github.com/PyCQA/autoflake/compare/v1.4...v1.7.1)
- [github.com/PyCQA/flake8: 4.0.1 → 5.0.4](https://github.com/PyCQA/flake8/compare/4.0.1...5.0.4)
- [github.com/asottile/pyupgrade: v2.34.0 → v3.0.0](https://github.com/asottile/pyupgrade/compare/v2.34.0...v3.0.0)
<!--pre-commit.ci end-->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6870ec5381e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.