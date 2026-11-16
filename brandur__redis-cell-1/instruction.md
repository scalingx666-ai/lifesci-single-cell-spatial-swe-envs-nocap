# Issue

**Title:** Rename project to "redis-cell"

## Description

Unfortunately, while "redis-throttle" seems to be more of an apt name for
the project, the contention for this name is incredible, with probably a
good half dozen projects vying for the spot.

Here we rename to "redis-cell" which currently has no collisions on Google.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14ed08f06826`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.