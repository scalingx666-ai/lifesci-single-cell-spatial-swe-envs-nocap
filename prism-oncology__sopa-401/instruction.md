# Issue

**Title:** Aggregation refactoring

## Description

In this PR:
- `aggregate_channels `now returns an AnnData object with cell IDs and Channel names.
- Added a `drop_filtered_cells `option to keep filtered cells; when disabled, filtered cells are marked in `table.obs["passes_filtering"] ` instead of being removed.
- Shapes are no longer dropped from the `SpatialData` object when cells are filtered from the aggregation table.

Issue #398

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56025a5047b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.