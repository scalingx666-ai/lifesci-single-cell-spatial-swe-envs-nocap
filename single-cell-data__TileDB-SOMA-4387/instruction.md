# Issue

**Title:** [python/r] Update R version and changelogs

## Description

**Issue and/or context:** Closes SOMA-808

* Update R version number for 2.3.0 release.
* Fix deprecation errors associated to 2.3.0 version bump.
* Update NEWS/HISTORY and R version number.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `71e9cb989d2e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.