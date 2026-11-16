# Issue

**Title:** Update release workflow to dynamically find skills

## Description

Updates the release workflow to dynamically find and package all skill directories (those containing SKILL.md) instead of hardcoding specific skills.

This makes it easier to add new skills without needing to update the workflow each time.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fe2f7bd0da6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.