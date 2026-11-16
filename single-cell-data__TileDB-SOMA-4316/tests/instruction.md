# Issue

**Title:** [python] Use importlib.metadata.version instead of __version__

## Description

**Issue and/or context:** Closes SOMA-693

**Changes:**
Use `importlib.metadata` instead of `__version__` to get library versions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7f9debed6ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.