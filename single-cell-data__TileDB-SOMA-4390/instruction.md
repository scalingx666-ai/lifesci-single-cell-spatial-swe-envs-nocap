# Issue

**Title:** [Backport to release-2.3][python/r] Update R version and changelogs

## Description

* Update Python history

* Update R NEWS and version number

* Prevent eval of `what` args in lifecycle::deprecate_* calls

Wrap `what` in `I()` to prevent unintended evaluation of R6 objects. For example: lifecycle::deprecate_warn(what="SOMAExperiment$tiledbsoma_ctx", when="2.3.0")

* Remove internal calls to deprecated self$tiledbsoma_ctx

SOMACollectionBase was calling self$tiledbsoma_ctx, which triggered the deprecation warning from the active bunding.

* Suppress deprecation warnings in SOMATileDBContext tests

Added `withr::local_options(lifecycle_verbosity = "quiet")` to suppress deprecation warnings since we're knowingly testing the deprecated class.

* Update iterated reader tests to leverage new set_default_context()

* Update deprecation handling for `set_data_type()`

- Adjusted tests for `set_data_type()` to reflect deprecation policy

---------


(cherry picked from commit 60406df290c9979186adbb6c2a8c6f29fd6c2e5e)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `93f0295a0d75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.