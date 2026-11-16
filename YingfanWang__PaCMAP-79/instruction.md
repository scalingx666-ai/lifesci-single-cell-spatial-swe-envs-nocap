# Issue

**Title:** remove setuptools as dependency

## Description

right now, if you install `pacmap` into a completely fresh venv, it will fail to execute `import pacmap` due to the `import pkg_resources`. Starting with Python 3.8, the builtin `importlib` supplies the requisite functionality

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f38024b0c2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.