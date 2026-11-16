# Issue

**Title:** feat(pp): expose high-expression exclusion in preprocess

## Description

## Summary
- Expose `exclude_highly_expressed` on `ov.pp.preprocess()` for the `shiftlog` normalization path.
- Preserve existing backend defaults when the argument is omitted, while allowing users to explicitly disable high-expression exclusion.
- Add a regression test covering the bounded `log1p(target_sum)` behavior when exclusion is disabled.

## Notes
This addresses the follow-up request in . The new parameter defaults to `None` so existing CPU/OOM behavior and RAPIDS defaults are preserved unless users opt in with an explicit boolean value.

## Validation
- `uv run --no-sync python -m pytest tests/pp/test_preprocess_hvg_seurat_unboundlocal.py -q`
- aubagent pre-commit review: no findings

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `509b98432b03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.