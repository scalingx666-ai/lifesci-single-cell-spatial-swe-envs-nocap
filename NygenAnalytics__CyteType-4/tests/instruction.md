# Issue

**Title:** linked _init__.py to .toml and version history

## Description

Problem: session.info.show() displayed NA in version history for CyteType
Solution: add version history to __init__.py and then dynamically link __init__.py to pyproject.toml in order to update version history in one place

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be81bb5a9c77`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.