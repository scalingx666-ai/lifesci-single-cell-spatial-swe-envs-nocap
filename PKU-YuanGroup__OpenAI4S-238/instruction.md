# Issue

**Title:** fix(ui): preserve run location and modal ownership across delayed responses

## Description

## Summary

A failed run-location read must not report Local or erase the last confirmed cluster location and undismissed kernel-loss warning. Preserve that evidence with explicit loading/error states, disable mutations while the status is unknown, and offer Retry. Distinguish an unavailable profile catalog from an empty one.

Discard responses from older reads, session navigation, and superseded dialog openings. A delayed read or allocation/release result must not overwrite or close an artifact preview, Ketcher editor, or newer dialog using the shared modal.

This replaces #215 by dvd233. All seven original contributor commits are retained unchanged, including head `8841ffb6`. Commit `2e8c982d` incorporates current `main` (`abbb47a1`) and adds the modal-ownership repairs and regression coverage.

## Area

- [x] Web UI / frontend
- [x] Compute / remote execution
- [x] Tests / harness / CI

## Change Type

- [x] Bug fix
- [x] Test / harness

## Verification

Passed locally on the published head:

- `npm test --prefix frontend -- --run`: 1,630 tests, including 35 compute tests.
- `npm run build --prefix frontend`: both TypeScript projects and Vite passed; a second build reproduced the committed distribution.
- `uv run pytest -n auto --maxprocesses=4 --dist loadfile`: 11,938 passed, 26 skipped (Python 3.13, macOS).
- `uv run pre-commit run --all-files`: all hooks passed.
- `node tests/browser_smoke.mjs`: full Chromium workbench smoke passed, including a held compute response followed by opening the real Ketcher editor.
- `uv run python -m harness.cli run --tier pr --offline`: 38 scenarios passed.
- Response-route contract, bilingual directory documentation, source credential scan, and crosswalk evidence checks passed.

Hosted validation of `2e8c982d` is complete: **35 successful checks and 3 conditionally skipped nightly checks**, with no pending or failed checks. [CI run 39819627602](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/39819627602) and [Protocol fuzzing](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/39819627548) passed. This includes all four Python offline suites (3.10/3.12/3.13/3.14), frozen response shapes, Chromium/Firefox/WebKit, Team Mode, Stage 0, packaging, and Linux sandbox checks. CodeQL and automated review checks also succeeded.

The first WebKit attempt was cancelled during unusually slow Ubuntu dependency downloads. The unchanged WebKit job passed on a fresh attempt; the other successful results were retained. No code, assertion, or check was weakened to obtain a pass.

## Risk and Reviewer Focus

Review `frontend/src/features/sessions/compute.ts`, its tests, and `tests/browser_smoke.mjs` for retained evidence, warning dismissal, retry, and ownership of asynchronous modal updates. Four added regressions failed before the modal repair and passed afterward.

The browser fault fixtures model response failures and ordering; they do not establish live cluster allocation or scientific execution. No backend API, dependency, permission boundary, or allocation-deduplication behavior changes. The crosswalk's notebook-export evidence digest was re-audited after extending its browser evidence file.

## Checklist

- [x] Reviewed the complete diff; changes are scoped to run-location truthfulness and asynchronous UI ownership.
- [x] Workbench source and rebuilt distribution are committed together; legacy UI and vendored files are unchanged.
- [x] Relevant tests and real-browser checks passed; no tests/assertions were removed or weakened.
- [x] No hard third-party core import or default-suite live-resource requirement was added.
- [x] No secrets, private data, or local absolute paths are included.
- [x] No compatibility/composition hotspot facade was rewritten.
- [x] Documentation and evidence claims match the tested behavior.

AI-assisted review, repair, and verification. Merged into `main` as 01a232e367d4bda52ef13dd7c49e4b7e77e744bf at the repository owner's explicit instruction, using an administrative override of the pending independent Code Owner review. The squash merge credits dvd233 as a co-author, and all seven original contributor commits remain in this PR. Original PR #215 is closed as superseded.

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Medium Risk**
> Changes race-prone session UI and shared-modal behavior where wrong labels could mislead users about where code runs, but scope is frontend-only with no API or allocation semantics changes.
>
> **Overview**
> **Run-location UI** now treats compute status as a phased read (`loading` / `available` / `error`) with response validation, instead of silently treating failed or malformed GETs as Local. On errors it keeps the last confirmed cluster badge and undismissed kernel-loss banner, labels evidence as stale, disables run-location choices until status is known, and adds **Retry** for status and profile catalog reads (catalog failures are shown separately from “no profiles configured”).
>
> **Async safety** ties updates to session `_openGen`, per-dialog request ids, and checks that the shared `#modal` is still owned by the run-location flow (visible body, `_modalMode`) so late responses do not repaint after navigation, dismissal, Ketcher/artifact reuse, or a newer dialog/allocation.
>
> `computeStatus` in the timeline store is typed as `ComputeReadState`; compute copy strings move into module-local i18n. Coverage expands in `compute.test.ts` and a new **browser smoke** scene with mocked compute/profile routes; committed **Vite dist** assets and a plan-crosswalk evidence digest update accompany the frontend build.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 2e8c982d9054d5abca2b15032efeb9dd4e7b981c. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `abbb47a12713`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.