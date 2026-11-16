# Issue

**Title:** Allow dev notebooks

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [x] New feature (non-breaking change which adds functionality)

### Description
<!--- What does this PR achieve? -->
Allow pulling notebooks from `squidpy_notebooks@dev`.
Repo dispatch not yet implemented, will do slightly before new release.

### How has this been tested?
<!--- Describe how you've tested your changes: -->
N/A

### Closes
<!--- If applicable, add `closes #XXXX` below to auto-close the issue related to this PR: -->
...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5684208eaee0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.