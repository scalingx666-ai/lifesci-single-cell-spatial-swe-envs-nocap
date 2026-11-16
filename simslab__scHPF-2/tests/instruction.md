# Issue

**Title:** Make scHPF a package

## Description

This enables the following:

- installation, version tracking via pip: `pip install git+https://www.github.com/simslab/scHPF.git#egg=scHPF`
- automatic installation of dependencies
- access to the API from Python code (e.g. for more easily plugging into hyperparameter optimization)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfc4ab8d3288`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.