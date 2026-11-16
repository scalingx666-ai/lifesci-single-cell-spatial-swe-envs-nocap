# Issue

**Title:** Duplicate file handling

## Description

Add message for if file being downloading already exists/has already been downloaded.

Also add error handling if already-downloaded file had been corrupted, in which case file will be re-downloaded.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e87f702da0eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.