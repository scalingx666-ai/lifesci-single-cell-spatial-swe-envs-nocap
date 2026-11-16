# Issue

**Title:** [ci] Fix errors and warnings from nightly failure

## Description

**Issue and/or context:** Closes SOMA-627

**Changes:**
* Fix wrong variable name in `runs-on`
* Don't brew install packages that are already installed

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0d6f4689a87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.