# Issue

**Title:** [r] Fix `soma_type` inconsistency between arrays and collections

## Description

**Issue and/or context:** Collection types (SOMACollection, SOMAExperiment, SOMAMeasurement) returned a named string from `soma_type` and other metadata (e.g., `c(name = "SOMACollection")`), while array types returned an unnamed string. Resolves SOMA-803. 

**Changes:**

- Updated `c_group_get_metadata()` to store metadata values directly in the result list instead of wrapping them in a named sub-list
- Updated existing tests to remove permissive assertions that worked around the named character issue with stricter `expect_equal()` calls (i.e., removed patterns like `expect_equivalent(x$soma_type, ...)` and `expect_true(x$soma_type == ...)`)
- Added test coverage  `set_metadata()`/`get_metadata()` round-trips for SOMACollections similar to what we have in tiledbsoma-py
- Updated an interop test was using `x$name` to access metadata values, which depended on the old named-list wrapping. 

- Unrelated Codecov config fix: Added `carryforward: true` to the Python and R flags. Previously, R-only PRs (like this one) showed a project coverage drop because codecov was computing the total without Python's files. With carryforward, codecov will reuse the last known coverage for whichever flag didn't upload. 

**Notes for Reviewer:** Stricter test assertions and new metadata coverage was added *before* implementing the C++ fix. You can see an expected failures [here](https://github.com/single-cell-data/TileDB-SOMA/actions/runs/22781706050/job/66090965508).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7235234280b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.