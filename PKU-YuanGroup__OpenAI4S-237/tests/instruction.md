# Issue

**Title:** fix(provenance): never tag a str in place; carry string lineage on a copy

## Description

## Summary

On a tracked DataFrame, indexing a string assigned by the user could tag the shared literal and attribute an unrelated later write to the CSV. Exact strings are now never tagged in place; supported reader, JSON and indexing boundaries return an owned string carrier.

The carrier preserves lineage through direct writes, `str`, `print`, single-field formatting and direct `%s` formatting. Worker inspection and file-read observation unwrap only the registered carrier types with built-in slicing, so conversion hooks cannot execute during inspection. Pickle deliberately restores the plain value; copy and deepcopy retain the carrier.

This branch includes `main` at `c7b8fd07`, including #235's JSON non-finite constant protection and #233's Ollama integration. The PR targets `main`; the provenance patch is unchanged by the latest branch update.

## Validation

- Twelve new regression cases failed before the repair: nine string output conversions, a persistent-kernel lineage case, and two conversion-hook cases.
- Focused provenance, kernel, agent and gateway tests passed.
- Full local Python 3.13 offline suite: **12,036 passed, 43 skipped** on `71b65157` (8m56s).
- Python 3.10 string/kernel regressions: 44 passed.
- Complete pre-commit, strict mypy, bilingual directory documentation, source credential scan, 222 route contracts and all 38 offline harness scenarios passed on `71b65157`.
- After the latest branch update, all 1,658 frontend tests passed and the production build reproduced the committed assets without changes.
- Real Chromium workbench smoke passed. A focused browser flow also verified tagged string/bytes/list previews, unrelated writes without false inputs, and printed/f-string/percent outputs linked to the CSV. With Stage 8 enabled, a tagged path was recorded in Notebook `files_read`.
- Hosted CI on `71b65157`: **32 checks succeeded, 3 scheduled-only checks skipped, 3 pending, no failures** at the latest check. All required checks passed. Chromium and the two Cursor checks are still running. .

## Limits and reviewer focus

This changes exact type identity for strings returned by supported reads: they are `str` subclasses. Plain-separator `join`, multi-field string assembly, tuple-based percent formatting and non-string aliased values remain bounded limitations documented with completion criteria in the bilingual TODO. No general alias-detection claim is made.

Review `provenance.py`'s carrier conversions and `worker.py`'s exact-type unwrapping. Core remains stdlib-only; worker changes are surgical; no tests were removed and vendored assets were not reformatted. No route, frontend source, dependency lock or kernel protocol change is included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7b8fd07ef0f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.