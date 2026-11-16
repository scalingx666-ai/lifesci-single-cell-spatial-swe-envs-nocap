# Issue

**Title:** Bump version in setup.py to match latest release

## Description

Latest releases (>0.2.0) haven't update the version on the package inside setup.py. 
Thus, when checking the installed package version (ie: `pip show cellbender`) people still see `0.2.0` even when the release `0.2.2` has installed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d82893c05b4e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.