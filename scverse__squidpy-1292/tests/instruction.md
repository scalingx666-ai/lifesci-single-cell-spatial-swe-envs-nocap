# Issue

**Title:** fix: preserve SpatialData input when copying spatial neighbors

## Description

## Description

Building spatial neighbor graphs from a `SpatialData` object with `copy=True` currently writes computed centroids into the original table before returning the graph. This can overwrite existing coordinates, add a new coordinate key, or leave changed coordinates behind when graph construction fails.

Pass `copy` through the shared input preparation path and use a temporary AnnData containing observation metadata and the metadata needed for legacy graph dispatch. This keeps computed coordinates out of the original table without copying or loading expression matrices, including for backed tables. The change covers the legacy function and all five current graph-building entry points. `copy=False` retains its existing behavior.

## How has this been tested?

- 91 tests passed across `tests/graph/test_spatial_neighbors_copy.py` and the existing `tests/graph/test_spatial_neighbors.py` on Python 3.13/macOS.
- The initial 28 regression cases failed against upstream before the fix.
- Coverage includes existing and missing coordinates, default and custom spatial keys, construction failures, read-only backed tables and unchanged files on disk, all six entry points, and multiple libraries. Returned graphs are compared with the in-place path.
- All applicable repository pre-commit checks and `git diff --check` passed.
- Full Sphinx HTML build passed with warnings treated as errors (`-W`); verified the generated release note.

## Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bdc22f54cc2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.