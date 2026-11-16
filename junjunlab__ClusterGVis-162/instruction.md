# Issue

**Title:** Fix installation error: relax R version dependency

## Description

The current dependency R (>= 4.5) prevents installation on the latest stable R version (4.4.x). Relaxing this requirement allows users to install the package on current standard environments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9266a8af9232`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.