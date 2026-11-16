# Issue

**Title:** Add cxg_immune_cell_atlas dataset to common test resources

## Description

## Describe your changes

Adds the CELLxGENE immune cell atlas as a new common test resource. This is required for adding foundation models to tasks which require human data and (for at least the batch integration task) the `.obsm["X_pca"]` slot to be filled.

## Checklist before requesting a review
- [x] I have performed a self-review of my code

- Check the correct box. Does this PR contain:
  - [ ] Breaking changes
  - [x] New functionality
  - [ ] Major changes
  - [ ] Minor changes
  - [ ] Bug fixes
  - [ ] Documentation

- [ ] Proposed changes are described in the CHANGELOG.md

- [ ] CI Tests succeed and look good!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bf274d8279e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.