# Issue

**Title:** {ts} update version import

## Description

Directly import `__version__` from package where needed rather than modifying `sys.path` and importing from `version.py`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb27867cef7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.