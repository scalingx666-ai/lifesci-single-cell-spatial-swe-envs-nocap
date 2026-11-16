# Issue

**Title:** Handle metric direction in `process_task_results`

## Description

## Describe your changes

Minor changes to steps in the `process_task_results` workflow so that metric direction is handled properly. Metrics that should be minimised should now correctly show high scaled scores for low raw scores.

## Checklist before requesting a review
- [x] I have performed a self-review of my code

- Check the correct box. Does this PR contain:
  - [ ] Breaking changes
  - [ ] New functionality
  - [ ] Major changes
  - [ ] Minor changes
  - [x] Bug fixes
  - [ ] Documentation

- [ ] Proposed changes are described in the CHANGELOG.md

- [x] CI Tests succeed and look good!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6729bf63b7e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.