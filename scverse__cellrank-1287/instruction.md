# Issue

**Title:** chore: deduplicate copilot instructions, gitignore uv.lock

## Description

Update the copilot instructions. 

Also adds `uv.lock` to `.gitignore` — library repos shouldn't commit lock files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb8bf09be829`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.