# Issue

**Title:** merge devel into master

## Description

### General
- Deprecated `--lamanno` and `--nucleus` flags. Use `--workflow` instead.
- Updated `setup.py` so that tests don't get installed.
- Fixed an issue where `requirements.txt` would not be included in the Pypi upload.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee106dd5c963`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.