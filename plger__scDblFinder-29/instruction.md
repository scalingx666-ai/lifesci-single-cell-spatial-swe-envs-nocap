# Issue

**Title:** Refer to the right internal function in tests.

## Description

Well, that was embarrassing; a copy-paste error that went unnoticed until I deleted some functions from **scran** in BioC-devel.

. I'll have to put **scDblFinder** on my wall to track its status.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d835404749d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.