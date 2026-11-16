# Issue

**Title:** [ci] Rename CI jobs and replace xcode action with brew install

## Description

**Issue and/or context:** Towards SOMA-410

**Changes:**
* Replace xcode action with brew install
* Rename some of the CI jobs for easier discovery in `Actions` tab

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca87c4da2f46`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.