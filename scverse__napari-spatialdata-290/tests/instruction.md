# Issue

**Title:** miant: Add depenabot configuration

## Description

This PR adds dependabot configuration to automatically bump versions of used actions and prevent failure of CI because of using outdated actions. 

It is scheduled to be monthly to avoid to often PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `682c26e8c01f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.