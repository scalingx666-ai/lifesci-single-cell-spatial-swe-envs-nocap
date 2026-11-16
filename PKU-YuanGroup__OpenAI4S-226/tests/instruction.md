# Issue

**Title:** fix(session-export): answer a package refusal with 409, not 500

## Description

## Summary

`GET /api/v1/frames/{fid}/session/export` did not translate `SessionPackageError`. That error is how the package boundary refuses, on purpose, to publish state it cannot package faithfully. Because nothing caught it, a deliberate refusal fell through to the dispatcher's catch-all and answered `500 {"code":"internal_error"}` with the reason withheld. The import and share routes already translate the same error.

The route now answers **`409 session_not_exportable`**. The body carries the refusal's own message, which is the same author-written domain text import and share already send:

```json
{"error": "Auto Mode turn references an unknown identity", "code": "session_not_exportable", "status": 409, "request_id": "…"}
```

**Can a real Auto Run be started for a turn with no action group? No.** So the fix is the status mapping. How the export derives turn ids is unchanged:

- `run_message` calls `action_ledger.append_user(...)`, which commits the turn's `kind="user"` action group, before `scientific_review.begin_turn_run(...)` starts the run.
- Every `store.start_auto_mode_run` call passes `action_ledger.turn_id`. That covers `begin_turn_run`, and `open_review_run` via `shadow_after_turn`, `gate_after_turn` and `persist_review_result`.
- Action groups are append-only. Nothing deletes them.
- Import remaps run turn ids through the same `turn_map` it builds from the imported groups.
- Checked with a real `run_message` and Auto Mode on:
  - A turn ended by a sole `finalize_response` writes `user`, `finalize` and `terminal` groups and exports 200.
  - A turn paused by the Auto Budget before any action was routed still has `user` and `terminal` groups and exports 200.

So the orphan-turn state from the report can only be created by writing to the Store directly.

**The same 500 can happen in production for other export refusals.** For example, a daemon that dies between a revert's barrier and its outcome leaves `session workspace revert requires recovery before export`. That answered 500 at base and now answers 409. Package-limit and integrity refusals get the same mapping.

## Area

- [x] Server / gateway / API
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix

## Verification

Validated at `025a64e293f5035605606a857810f6380edc151b`, after synchronizing with `main` (`7d0cf3db`). No additional product-code defect was found in the exception translation.

Ran:

```text
uv run pytest tests/test_session_export_refusal.py tests/test_session_package.py tests/test_auto_mode_portability_regressions.py tests/test_gateway_session_domain_routes.py
# 140 passed

uv run python scripts/capture_response_schemas.py --check
# Full offline suite: 11399 passed, 34 skipped, 2 warnings (554.83 seconds)
# 215/215 routes exercised; no breaking response-shape change
# Additive differences only in artifact versions, remote compute,
# project action-timeline, and project lineage; no export-route drift.

uv run python scripts/capture_response_contract.py --check
# Contract up to date: 215/215 routes

uv run python -m harness.cli run --tier pr --offline
# 38/38 passed (26 contract-only, 12 production-backed)

uv run python scripts/check_directory_readmes.py
# Complete bilingual coverage: 171 maintained directories, 1762 direct files/assets

uv run python scripts/source_secret_scan.py
# Passed: 4098 files

uv run pre-commit run --all-files
# Passed, including strict core mypy and CSS-token checks

node tests/browser_smoke.mjs
# Passed against ./start.sh in a disposable data directory and loopback port,
# using the pinned Playwright driver and Chromium; includes session ZIP export/import.
```

Additional real HTTP socket validation confirmed: unauthenticated requests return 401; unknown sessions return 404; an interrupted-revert refusal returns the exact 409 envelope with a request ID and no ZIP/download headers; refusal releases the execution lease; removing the recovery barrier permits a 200 ZIP with a matching SHA-256 header.

Not run locally:

```text
Container smoke, Windows tests, Linux bubblewrap smokes, Firefox/WebKit browser suites
```

Reason:

```text
Local validation used macOS and Chromium. Cross-platform results are reported by
the fresh hosted checks on this exact head. Skipped nightly jobs and the neutral
Bugbot run (usage limit reached) are not counted as passes.
```

Hosted validation: [CI run for this head](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38255664336).

Final hosted result on this head: **34 successful checks, 0 failures, 0 pending**; 3 nightly jobs skipped and Bugbot neutral because its usage limit was reached. All required checks passed. Code Owner approval is still pending; this PR has not been merged.

## Risk and Reviewer Focus

- `openai4s/server/gateway.py`, the `session/export` branch: every `SessionPackageError` raised by the export changes from 500 to 409. That includes the defensive race check (`session active branch or head changed during export; retry`), which keeps its "retry" text under the same code. Export already holds the session's FIFO execution lease, so that check is a backstop rather than an expected path.
- Response artifacts: the error body uses the existing envelope, and the frozen `[error]` shape for this route already matches, so `docs/response-schemas.json` is unchanged. `docs/response-contract.json` records only statuses the prober can elicit. A 409 needs a refused session state the prober does not seed, so per repo convention the entry stays `[200, 404]` and is not hand-edited. The route-level tests are the evidence for 409.
- Out of scope, left as they are:
  - A delegated child frame id on session routes still answers 500 (`SessionRunner._state` raises a bare `ValueError`). It is tracked separately.
  - Share create/update answer this same refusal as `400`.
  - The workbench export link (`<a download>`) does not show the refusal text.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py` (one `try/except` in the route).
- [x] Workbench changes: none.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site.
- [x] New dependencies, if any, are documented and justified (none).

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual verification notes (n/a).
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior (`docs/webapp-api.md` export rows, `docs/auto-mode.md`).
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected (`tests/README.md` and `tests/README_zh.md` rows added).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Single exception translation on an existing read-only export route; behavior for exportable sessions is unchanged aside from clearer errors when packaging refuses.
>
> **Overview**
> **Session export** now maps `SessionPackageError` to **`409 session_not_exportable`** with the package boundary’s domain message, matching import/share behavior instead of a generic **`500 internal_error`**.
>
> Docs state that export is **fail-closed** (no partial ZIP) for unresolvable Auto Mode ledger state, pending revert recovery, limits, and similar refusals. New route-level tests in `test_session_export_refusal.py` cover orphan Auto Mode runs, revert-awaiting-recovery, successful export after a real turn, and lease release on refusal.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 025a64e293f5035605606a857810f6380edc151b. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d0cf3db9d92`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.