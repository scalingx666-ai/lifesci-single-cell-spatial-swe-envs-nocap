# Issue

**Title:** Fix CI and docs building

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [ ] New feature (non-breaking change which adds functionality)

### Description
<!--- What does this PR achieve? -->
Regenerate `.pickle` files for `pandas==1.3.0` and pin `sphinx` because of `nbhpinx`.

### How has this been tested?
<!--- Describe how you've tested your changes: -->
NA

### Closes
<!--- If applicable, add `closes #XXXX` below to auto-close the issue related to this PR: -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e3dca848359`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.