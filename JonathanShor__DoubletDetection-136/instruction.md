# Issue

**Title:** move to poetry for dist, remove excess code, use pip installable pheno

## Description

- Allow distribution to PyPI with poetry
- Add doublet_score function which has been used for benchmarking in other papers
- Add basic testing
- Remove data loading functions (mature software like scanpy handles this now)
- Remove umap plot function (again defer to scanpy)
- Refresh tutorial

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b784798770e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.