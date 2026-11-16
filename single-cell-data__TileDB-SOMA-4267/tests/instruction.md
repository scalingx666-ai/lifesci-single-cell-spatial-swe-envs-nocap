# Issue

**Title:** Substitute macos-13 runners with macos-15-intel

## Description

**Issue and/or context:**
The `macOS 13` runner image will be retired by `December 4th, 2025`. To raise awareness of the upcoming removal, jobs using `macOS 13` will temporarily fail during the scheduled brownout.

**Changes:**
- Changed the `macos-13` with `macos-15-intel` which is newly introduced label for environments that require the x86_64 (Intel) environment
- 
**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4979aabe2aa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.