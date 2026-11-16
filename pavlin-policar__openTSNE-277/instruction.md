# Issue

**Title:** Knn params

## Description

##### Issue
 (cont).


##### Description of changes
Fixes things up from #265:
- Add tests.
- Fix bug where `knn_index` was passed instead of `knn_kwargs`
- I removed `test_building_with_gt15_calls_query` since it was actually not doing what it was supposed to, and it was implementation specific. I don't think that it makes sense to test what the test was actually testing.


##### Includes
- [X] Code changes
- [X] Tests
- [ ] Documentation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37776dcbcc70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.