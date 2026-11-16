# Issue

**Title:** Setting get_spatialdata_registry() known hash to None

## Description

modified:   src/harpy/datasets/registry.py to set known hash in `get_spatialdata_registry()` definition to `None` from e5eac7dbe316ad7008822fde95c1abacfcfc771b8f9ab28c0e6f768d293cd8d5. . @berombau

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37d8cfe7d35f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.