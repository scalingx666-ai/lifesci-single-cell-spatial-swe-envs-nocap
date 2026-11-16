# Issue

**Title:** RTD fixes ahead of new documentation

## Description

RTD now requires a .readthedocs.yml (seems it has for several years). Added this file, and also fixed the docs/requirements.txt and conf.py so that imports are mocked rather than having to install dependencies to build the documents.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee39b777ee69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.