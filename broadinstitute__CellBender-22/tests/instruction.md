# Issue

**Title:** Refactorings to allow a low-profile build for RTD integration

## Description

Stripped down requirements for RTD build
Refactored tool argparse from tool CLI
Renamed a few CLI-related source files

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `979fb3d35f89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.