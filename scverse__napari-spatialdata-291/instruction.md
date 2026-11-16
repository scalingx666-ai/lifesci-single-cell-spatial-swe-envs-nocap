# Issue

**Title:** Modernize release workflow use most recent tool

## Description

This PR is modernizing release workflow (and allowing for future switch into trusted publishers) to use most recent tools best practices. 

- [ ] The main missing thing is to cut information from the changelog file and provide it as a body.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `682c26e8c01f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.