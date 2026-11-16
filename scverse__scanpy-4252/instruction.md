# Issue

**Title:** fix(plotting): keep boolean colors stable after subsetting

## Description

Release notes are included in `docs/release-notes/4219.feat.md`

## Summary

This draft PR adds support for mappings stored in `adata.uns[f"{key}_colors"]`, so boolean colors can stay tied to `True`/`False` after subsetting.

Existing list-based color behavior is preserved.

## Testing

Added tests for:
- mapping palettes stored in `adata.uns`
- boolean mappings after subsetting to only `True` or only `False`
- boolean mappings passed through the explicit `palette=` argument
- regression test for #4219 covering boolean color mappings in `adata.uns` after subsetting.

Local checks run:
- `ruff check`
- `ruff format --check`
- `python -m py_compile`
- `git diff --check`

I could not run `pytest` locally due to local environment issues, so I am opening this as a draft for CI and maintainer feedback.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15d8fb103d94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.