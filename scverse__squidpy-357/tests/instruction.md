# Issue

**Title:** allow diagonal setting in spatial_neighbors

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [x] New feature (non-breaking change which adds functionality)

### Description
<!--- What does this PR achieve? -->
exposing `set_diag` to the end-user. Example usage in a complex GAT structure where one needs the diagonal to be 1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53f17eb87285`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.