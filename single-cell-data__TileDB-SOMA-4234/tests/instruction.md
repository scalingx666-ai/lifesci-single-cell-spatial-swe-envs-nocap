# Issue

**Title:** [ci] Change Python packaging CI in preparation for cibuildwheel changes

## Description

**Issue and/or context:** Towards SOMA-390

**Changes:**
* Remove Python CI packaging tests
* Split sdist and wheel build and testing into separate jobs
* Use brew instead of xcode action to get macos dependencies

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e0b516c9f91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.