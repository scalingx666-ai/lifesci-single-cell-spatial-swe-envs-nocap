# Issue

**Title:** Fix CI script

## Description

The @master branch was removed from https://github.com/actions/upload-artifact, so I pinned it to v3 instead. Similarly, I pinned the https://github.com/r-lib/actions action to v2.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `038eb8a9671b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.