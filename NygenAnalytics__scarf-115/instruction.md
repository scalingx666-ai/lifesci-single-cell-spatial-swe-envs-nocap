# Issue

**Title:** Fixes for parallell runs

## Description

* Create `markers/{slot_name}` early in `run_marker_search` so other processes can detect that marker search is in progress for this slot.
* Add `try` in `__get_size` for Metadata. This mitigates issues that can happen when another process is currently writing a zarr group to the hierarchy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `440bab17db73`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.