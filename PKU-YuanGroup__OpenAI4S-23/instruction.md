# Issue

**Title:** fix(skills): re-enumerable protein-mutation loop seeds + clearer parsing errors

## Description

## Summary

Delivers to `main` the fix that PR #21 was intended to carry but did not: PR #21 merged the original `protein-mutation-enhancement` code **without** this fix, leaving a blocking bug in `main`.

### Fixes
- **[blocking]** `run_selection_round` returned `next_round_seeds` as ranked variant dicts (no top-level `position`); feeding them back into `enumerate_mutants` — exactly as the SKILL Loop Pattern documents — raised `TypeError` on round 2. Now returns canonical variant IDs.
- `_coerce_mutation`: validate 1-indexed positions via a new `_residue_at` helper; raise a clear `ValueError` (instead of `IndexError` / `int(None)` `TypeError`) for out-of-range or position-less inputs.
- `rank_mutants`: move the empty-weights guard ahead of the default substitution so an explicit `weights={}` is actually rejected (was dead code).

### Tests
Adds 4 fixture-based regression tests (loop re-enumeration, empty-weights rejection, out-of-range tuple, position-less variant dict). Targeted suite passes; pre-commit (black/isort/ruff) green.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `062641923f8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.