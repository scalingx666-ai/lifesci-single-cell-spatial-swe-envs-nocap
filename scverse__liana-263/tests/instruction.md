# Issue

**Title:** Remove bumpversion

## Description

Drops the `.bumpversion.cfg` left over from the template transition, along with the `bumpversion` dev dependency and its section in the contributing docs.
Since the config was the only thing keeping `liana.__version__` in sync with `pyproject.toml`, `__version__` is now read from the installed package metadata.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `120e7a75f502`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.