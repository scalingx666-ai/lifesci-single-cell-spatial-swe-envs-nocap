# Issue

**Title:** Patch release preparation

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [ ] New feature (non-breaking change which adds functionality)

### Description
<!--- What does this PR achieve? -->
Prepare patch release so that we can have stable/latest docs.

### How has this been tested?
<!--- Describe how you've tested your changes: -->
N/A

### Closes
<!--- If applicable, add `closes #XXXX` below to auto-close the issue related to this PR: -->
N/A

TODOs:
- merge prepare dev #365 
- revert master to `5a53dfd299fcde82ea74fea05a1a7f9ae8a30c12` (just before moran from scanpy)
- enable stable on RTFD
- change latest -> stable in `squidpy` and `squidpy_notebboks` GH
- make new release (1.0.1)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a53dfd299fc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.