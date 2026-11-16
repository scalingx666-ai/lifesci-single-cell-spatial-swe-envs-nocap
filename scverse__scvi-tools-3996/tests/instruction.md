# Issue

**Title:** Backport PR #3995 on branch 1.5.x (fix(model): resolve BaseModelClass.view_registry  AttributeError and align _registry/registry access)

## Description

Backport PR #3995: fix(model): resolve BaseModelClass.view_registry  AttributeError and align _registry/registry access

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `972c5b7776e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.