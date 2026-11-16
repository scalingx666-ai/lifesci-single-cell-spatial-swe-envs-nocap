# Issue

**Title:** [r] Test coverage for duplicate key behavior in SOMA collections

## Description

## Issue and/or context

[SOMA-818](https://linear.app/tiledb/issue/SOMA-818/r-add-test-coverage-for-duplicate-key-behavior-in-soma-collections)

## Changes

Add test coverage for duplicate key handling in R SOMA collections via `write_soma()` and `SOMACollection$set()`.

- Added two new test cases for `SOMACollection$set()` to:
  - verify that attempting to add a member with an existing key within the same session throws an error and the original member is preserved
  - verify the same duplicate key rejection behavior persists after closing and reopening the collection
- Both tests also verify that `add_new_*` methods reject existing keys with "Member 'foo' already exists" error

- Added test case for `write_soma()` to:
  - verify that `write_soma()` emits an `existingKeyWarning` condition when attempting to register an object with a duplicate key (when `verbose = TRUE`)
  - confirm the original data was preserved and not replaced

## Notes for Reviewer

The new tests revealed a bug in R's `SOMACollectionBase$set()` method. The test at `test-06-SOMACollection.R:245` was expected to throw an error but it actually allowed replacing an existing member after reopening the collection (see test failure [here](https://github.com/single-cell-data/TileDB-SOMA/actions/runs/21215626427/job/61036334902?pr=4378#step:7:524).

```r
collection$set(sdf1, name = "foo")
collection$close()
collection <- SOMACollectionOpen(uri, mode = "WRITE")
collection$set(sdf2, name = "foo")  # No error - silently allows replacement
```

This behavior differs from Python's `Collection.__setitem__()`, which correctly raises an error when attempting to add a duplicate key, both within the same session and after reopening the collection.

```python
collection["foo"] = obj1
collection["foo"] = obj2  # Raises SOMAError: "replacing key 'foo' is unsupported"
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b521daece970`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.