# Issue

**Title:** Update WDL and setup.py version

## Description

Small updates to WDL.  Default to "nvidia-tesla-t4", which will be cheaper/faster than a K80.

Update cellbender version number in `setup.py`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f93d67b6e2d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.