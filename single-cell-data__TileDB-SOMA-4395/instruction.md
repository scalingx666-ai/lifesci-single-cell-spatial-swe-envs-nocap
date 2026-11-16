# Issue

**Title:** [r] Skip tests using deprecated code in envs with lifecycle < 1.0.5

## Description

**Issue and/or context:** [SOMA-845]

**Changes:**

 1. `test-03-SOMATileDBContext.R`: Added `skip_if_not_installed("lifecycle", minimum_version = "1.0.5")` to test blocks that use `expect_no_condition()` with deprecation warnings.
 2. `DESCRIPTION`: Removed duplicate lifecycle entry.

**Notes for Reviewer:** In lifecycle 1.0.4, `deprecate_warn()` unconditionally called `signal_stage("deprecated", what)` before checking the lifecycle_verbosity option. This emitted a `lifecycle_stage` condition even when lifecycle_verbosity = "quiet". In 1.0.5, , fixing the issue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f4ab22ff44a7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.