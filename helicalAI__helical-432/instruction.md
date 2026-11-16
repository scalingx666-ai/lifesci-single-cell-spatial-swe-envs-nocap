# Issue

**Title:** Merge main into release (v3.1.3)

## Description

## Summary

Merges `main` into `release`, bringing `release` up to v3.1.3.

Commits coming from `main`:
- `706c13f` feat(soc2type2): bump version to release soc2type2 change (#430)
- `e3478af` ci: add `ci` aggregator job as the single required status check (#424)
- `2a0b2c5` Removing an override of `logging.disable` that breaks third-party callers (#428)

## Conflict resolution

One conflict, in `pyproject.toml`:

| side | version |
|---|---|
| `release` | `3.1.2` |
| `main` | `3.1.3` |

Resolved to **`3.1.3`**. `release` was already at `3.1.2` because #428 was cherry-picked onto it as #429; `main` then bumped to `3.1.3` in #430, so `main`'s value is the newer one and supersedes it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `635cc8e983dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.