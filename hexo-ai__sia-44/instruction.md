# Issue

**Title:** Add GitHub issue and pull request templates

## Description

- Added a bug report issue form with reproduction, environment, task, agent implementation, sandbox mode, command, and log fields.
- Added a feature request issue form with use case, proposed solution, affected project area, alternatives, implementation notes, and contribution-interest fields.
- Added issue template configuration with a security-report contact link to `SECURITY.md`.
- Added a pull request template covering summary, change type, related issues, testing, security/privacy review, documentation, and contributor checklist items.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b141ced261c9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.