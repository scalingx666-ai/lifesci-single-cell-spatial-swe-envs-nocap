# Issue

**Title:** Move from setup.py to pyproject.toml

## Description

Following PEP 621, and due to the error I was running into here #239 , this PR moves from using setup.py to pyproject.toml for python packaging of cellbender.

This has successfully been used to build and publish cellbender 0.3.0 to PyPI.

I have single sourced the version in `/cellbender/VERSION.txt`
- For new versions, this file (and only this file) needs to be manually changed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `02dd763fdb3b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.