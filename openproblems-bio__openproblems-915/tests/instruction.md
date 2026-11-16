# Issue

**Title:** Update reporting components to include all links

## Description

## Describe your changes

* Update `get_task_info`, `get_method_info` and `get_metrics_info` comp with more info and extend output
* Fix bug in `process_task_results/run_test.sh` 


## Checklist before requesting a review
- [x] I have performed a self-review of my code

- Check the correct box. Does this PR contain:
  - [ ] Breaking changes
  - [ ] New functionality
  - [ ] Major changes
  - [x] Minor changes
  - [x] Bug fixes
  - [ ] Documentation

- [x] Proposed changes are described in the CHANGELOG.md

- [ ] CI Tests succeed and look good!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `927b5a66b482`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.