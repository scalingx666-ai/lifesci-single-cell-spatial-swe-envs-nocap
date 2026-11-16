# Issue

**Title:** [r] Add Carrara support to `write_soma` ingestion

## Description

**Issue and/or context:** [SOMA-758]

**Changes:**

- Updates the internal `.register_soma_object()` function to support both Carrara (TileDB v3) and TileDB v2 URIs.
- Expands tests coverage for Carrara to include Seurat object ingestion/reading.
- Adds test suite for legacy TileDB Cloud workflows to ensure continued compatibility.

**Notes for Reviewer:**

Other than the new tests, the biggest change is the refactor of `.register_soma_object()`. The original implementation was complex due to the need to:

1. Track and restore the mode (READ/WRITE/CLOSED) of both the object and parent collection
2. Use `on.exit()` to ensure original modes were restored
3. Perform a pre-check to see if a key already existed in the parent before attempting registration

The new implementation handles both Carrara and v2:

- For v3 URIS, Carrara automatically registers children with their parent collection when they're created at a nested URI, so no `set()` calls are required.
- For v2 URIs, instead of pre-checking existence (which required the mode tracking), we use `tryCatch()` to attempt registration and silently ignore "already exists" errors (matching Python's `_maybe_set()` helper in `tiledbsoma.io.ingest`) or throw a warning if `options(verbose = TRUE)` (matching the original behavior).

See the `README-cloud.md` for details on running the new cloud tests (recommended before merging).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ef58af0cd8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.