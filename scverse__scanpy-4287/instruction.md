# Issue

**Title:** chore: use frozendict on 3.15

## Description

Not adding `__lazy_imports__` yet, will do that once numba actually supports Python 3.15

- [x] [Release notes][] not necessary because: dev only change

[release notes]: https://scanpy.readthedocs.io/en/stable/dev/documentation.html#adding-to-the-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f3bdd263ef0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.