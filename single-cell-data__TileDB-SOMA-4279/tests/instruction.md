# Issue

**Title:** [r] Deprecate `SOMANDArrayBase$set_data_type()`

## Description

Deprecate unused public method. Also add new utilities for aiding in staged deperecation/defunct cycles

Modified SOMA methods:
 - `SOMANDArrayBase$set_data_type()`: deprecated

New internal helper functions:
 - `.deprecate()`: wrapper around `lifecycle::deprecate_warn()` and `lifecycle::deprecate_stop()` that automatically determines when to issue deprecation warnings or defunct errors
 - `deprecation_stage()`: test fixture to determine expected deprecation stage for testing. Returns a string with the expected stage so tests can switch between `lifecycle::expect_deprecated()` and `lifecycle::expect_defunct()`

```R
test_that("example test deprecation", {
  switch(
    expr = deprecation_stage("2.0.0"),
    deprecated = lifecycle::expect_deprecated(deprecated_function())
    defunct = lifecycle::expect_defunct(deprecated_function())
  )
}
```

Resolves [SOMA-537](https://linear.app/tiledb/issue/SOMA-537/r-deprecate-somandarraybasedollarset-data-type)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `307f9ee86c6b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.