# Issue

**Title:** Use low level Redis module APIs

## Description

Switch to use low level Redis module APIs (i.e. off of the more blunt `CALL`
API). Theoretically this should result in improved performance (but in practice
doesn't seem to make a huge difference),

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8adb53c306a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.