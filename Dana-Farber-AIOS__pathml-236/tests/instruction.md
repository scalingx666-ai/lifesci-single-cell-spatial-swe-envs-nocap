# Issue

**Title:** Versioning

## Description

Track version number in `pathml/_version.py`. Other places in the code where we need the version number, such as `setup.py` and `docs/source/conf.py`, we read the version number from that file. This will make it easier to track consistently. Also add a section in documentation about versioning. Also add `pathml.__version__` for users.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e4208736f29`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.