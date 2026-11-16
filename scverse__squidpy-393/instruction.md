# Issue

**Title:** Delaunay radius

## Description

### Types of changes
<!--- What types of changes are introduced? Put an `x` in all applicable boxes: -->
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] Breaking change (change that would cause existing functionality to not work as before)
- [ ] New feature (non-breaking change which adds functionality)

### Description
<!--- What does this PR achieve? -->
- `n_neighs` instead of `n_neigh`/`n_neigh_grid` (controls both grid/generic)
- `radius` can be specified as [min, max], keeps edges only in `[min, max]` interval (mb use `(min, max)`)
- `radius` in the above form can also affect graph from Delaunay triangulation
- fixed the rare bug in #386
- add `copy: bool = False`
- improve the docstrings

### How has this been tested?
<!--- Describe how you've tested your changes: -->
Add 2 tests: 1 for copy, 1 parametrized for radius as a tuple.

### Closes
<!--- If applicable, add `closes #XXXX` below to auto-close the issue related to this PR: -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67f59761fa58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.