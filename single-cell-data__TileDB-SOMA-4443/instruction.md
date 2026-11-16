# Issue

**Title:** [r] Document SOMACollectionOpen()'s stricter type checking

## Description

**Issue and/or context:** [SOMA-909]

This documents the breaking change introduced in [SOMA-909](https://linear.app/tiledb/issue/SOMA-909) where `SOMACollectionOpen()` now raises an error if the URI points to a `SOMAExperiment`, `SOMAMeasurement`, or other collection subtype.

**Changes:**

- Added a NEWS entry for the breaking change
- Updated `SOMACollectionOpen()` docs to explain the strict type-checking behavior and direct users to `SOMAExperimentOpen()`, `SOMAMeasurementOpen()`, or `SOMAOpen()` as appropriate
- Expanded `SOMAOpen()` docs to clarify that it auto-detects the SOMA type and returns the correct subclass, making it the safe choice when the type is unknown
- Fixed two tests in `test-carrara-01-create.R` that were opening `SOMAExperiment` and `SOMAMeasurement` URIs via `SOMACollectionOpen()`
- Minor: fixed a broken cross-reference in `utils-arrow.R` roxygen docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60d227e9c340`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.