# Issue

**Title:** Additional minor changes needed for 1.2.0

## Description

Adds the below items:

- Cleans up the kit selection for BLAZE so its more scalable
- Fixes the BLAZE file container conditional to match other module files
- Fixed issue where whitelist could not be gzipped

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e85516dd7c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.