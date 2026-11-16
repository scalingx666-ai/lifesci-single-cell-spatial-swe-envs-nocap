# Issue

**Title:** [python] Add medium_runner pytest mark to prevent macos OOM errors on CI

## Description

**Issue and/or context:** Closes SOMA-392

**Changes:**
This adds a pytest "medium_runner" tag that is used to filter tests for the MacOS runners. We can add/remove this mark to tests as we see what triggers the CI OOMs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35e9fddcd45a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.