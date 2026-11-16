# Issue

**Title:** [cpp] Improve invalid type error and clean-up SOMAGroup initialization

## Description

**Issue and/or context:** Closes SOMA-673

**Changes:**
* Move a function only used in group.cc from `util.h` to `group.cc`.
* Modify the function and error message to be more specific to its usage in `group.cc`.
* Convert `SOMAGroup::fill_cache` to two helper functions that produce member components without side-effects.

**Notes for Reviewer:**
The error referenced in SOMA-673 was likely from a different instance of the same error message that was already modified. This particular error should only be hit if a future version of TileDB adds in a new object type that can be added to groups.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `04b4d451e1f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.