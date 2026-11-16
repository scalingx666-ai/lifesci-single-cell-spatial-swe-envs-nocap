# Issue

**Title:** Add links to tiledb academy tutorials

## Description

**Issue and/or context:** Now that all notebooks have been migrated to [TileDB Academy](https://cloud.tiledb.com/academy) we need to make this content more discoverable from the rtd site.

**Changes:**

- Removed dangling symbolic links to previously deleted notebooks
- Removed remaining distributed scanpy notebook
- Removed reference to deprecated `create_from_matrix` function
- Added individual links to relevant tiledb academy guides and tutorials

**Notes for Reviewer:**

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4979aabe2aa3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.