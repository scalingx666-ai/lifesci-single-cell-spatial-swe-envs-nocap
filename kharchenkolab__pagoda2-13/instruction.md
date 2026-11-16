# Issue

**Title:** Multicore Rtsne, minor fixes

## Description

- added Rtsne.multicore support
- moved away from myGOTERMS
- fixed broken pagoda2 copy constructor
- switch to much faster urltools::url_decode()

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9e8306d88728`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.