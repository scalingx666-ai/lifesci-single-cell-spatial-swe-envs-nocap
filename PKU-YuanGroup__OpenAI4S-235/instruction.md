# Issue

**Title:** fix(provenance): exclude known shared constants from lineage tags

## Description

## Summary

Reading a tracked JSON scalar or indexing a tracked DataFrame could attach a source tag to a process-wide constant. A later, unrelated write of the same object then reported a file it never read as an input.

`set_tags` now refuses known shared constants before touching either object attributes or the identity side table:

- Interpreter singletons, cached small integers, empty/one-character strings and bytes, and the empty tuple.
- The standard-library JSON decoder's shared `NaN`, `Infinity`, and `-Infinity` objects.
- NumPy's `True_`/`False_`/`nan` and pandas' `NaT`/`NA`.

The integer check follows the running interpreter's cache rather than hard-coding bounds. Library constants are looked up in already-loaded modules; the core gains no dependency.

## Regression coverage

`tests/test_provenance_shared_objects.py` covers independent reads and unrelated writes, with positive controls for values owned by an actual read. It also exercises the real Kernel, HostDispatcher, and Store across two cells: reading tracked non-finite JSON in one cell must not create lineage for an independent parse saved in the next.

The three non-finite parse cases and the real-kernel regression all failed on the previous PR head for false lineage, then passed after the fix. The kernel regression also checks that unrelated output files were actually written.

## Validation at `17ae5293`

- Focused provenance, kernel, agent, and gateway tests passed.
- The shared-object suite passed on Python 3.10 and 3.13 with the science dependencies. A separate stdlib-only check passed without importing NumPy or pandas.
- Full local Python 3.13 suite: **11,956 passed, 43 skipped, 1 failed**. The failure was the macOS sandbox test that accesses `https://example.com`; the unchanged test passed when rerun on this commit and separately on current `main`, using the same interpreter. The test and sandbox implementation are identical on both branches. This is recorded as a first-run failure with successful isolated reruns, not a fully green first run.
- Full pre-commit, strict mypy, bilingual directory documentation, source credential scan, and all 38 offline harness scenarios passed.
- The real Chromium workbench smoke passed against this checkout's daemon.
- Hosted validation: [CI run for this commit](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/39913934074).

The branch includes current `main` at `d0fa78b8`. No routes, response serializers, frontend source, dependency locks, or kernel protocol were changed by this fix.

## Known limitation and reviewer focus

This is a guard for known constants, not a general alias detector. Longer interned strings can still acquire false lineage when broadcast into a tracked DataFrame and then indexed. The residual is now tracked with completion criteria in [docs/TODO.md](https://github.com/PKU-YuanGroup/OpenAI4S/blob/fix/provenance-shared-singleton-tags/docs/TODO.md#provenance) and its Chinese counterpart; it is not claimed fixed here.

Review the shared-object identity predicate, positive lineage controls, and the persistent two-cell regression. Core remains stdlib-only, compatibility facades were not rewritten, vendored content was not reformatted, and no tests were deleted.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0fa78b88769`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.