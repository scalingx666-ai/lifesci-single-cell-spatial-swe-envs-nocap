# Issue

**Title:** [r] Add Carrara test coverage for duplicate key behavior

## Description

**Issue and context:** [SOMA-824] This is a follow-on to #4378, which added test coverage for duplicate key handling in the R package. This PR adds coverage specifically for Carrara.

**Changes:**

- `.check_soma_uri()`
  - added an optional `key` parameter used to ensure a collection member name matches the object's URI basename when writing to Carrara
  - this validation occurs before object creation to avoid leave the collection in an invalid state

- `test-carrara-03-uri-enforcement.R`
  - added tests verifying that `write_soma()` rejects mismatched key/URI combinations
  - verified that when `key` is omitted, the URI basename is correctly used as the member name
  - confirmed successful writes when key matches URI basename

- `test-carrara-04-error-handling.R`
  - added tests to verify`SOMACollection$add_new_*()` rejects duplicate keys before and after closing/reopening
  - added tests to verify `write_soma()` errors when attempting to write to an already-existing URI/key

**Notes for reviewer:** Also removed a warning from `.check_soma_uri()` that appears to be a debug leftover.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a464795d6519`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.