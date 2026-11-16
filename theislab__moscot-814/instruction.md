# Issue

**Title:** Align method assignment fix

## Description

Turns out the bug was because of the way the results are assigned to adata.

Fixes    and adds tests to it. The test fails on the unfixed version. You can also checked the corrected visualization from my comment 

The problem was the assignment.
```python
aligned_basis = np.vstack([aligned_maps[k] for k in self._policy._cat])
# the order of adata and the order of self._policy didn’t match
self.adata.obsm[key_added] = aligned_basis
```
So in this PR I made sure to assing the adata by the batches correctly

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bdfe28f87986`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.