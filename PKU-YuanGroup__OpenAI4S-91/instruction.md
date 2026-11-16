# Issue

**Title:** ui: complete the trajectory ledger view

## Description

## Summary

Completes the Action Timeline rewrite into a virtualized **trajectory ledger**: a windowed table over the durable Action Ledger, an SVG timing overview (queue / first-response / decode phases) with drag-to-filter, wheel-zoom and pan, loaded-scope search, and per-turn folding. Two commits:

- `1bb1530` — the ledger view itself (app.js, style.css, browser + static-contract coverage).
- `a08e889` — fixes from a review pass over that commit, listed below.

### Fixes in the second commit

The recurring theme is the surface presenting **unknown state as known**, or hiding state it should show.

- **A time brush hid every action with no execution attempt.** `filteredActionTimelineGroups` resolved each group through the SVG paint model, and `actionTimelineSelectionOverlaps` returned `false` for anything absent from it. Reproduced against a real `Store`: `user` and `permission_resolution` groups project `attempts: []`, so dragging any range — even one spanning the whole domain — silently dropped every user turn, permission decision, native tool call and finalize from the ledger. Now falls back to the group's own `created_at`.
- **Attempts were queried without `branch_id`.** `list_attempts` defaults it to `root_frame_id`, so on any forked branch every group projected `attempts: []` — a blank chart and no durations. Reproduced against a real `Store`; fixed by passing the branch through, with a regression test that was falsified against the unfixed code (it fails `assert [] == ['cell-fork']`).
- **The Tokens cell printed a fabricated `0`** whenever `usage` was absent, though the server returns `null` for every group that carried no model reply — and the same row's Duration cell already used an em dash.
- **Row status was icon colour only.** CSS styled two of the six server statuses, so `cancelled` / `pending` / `running` / `recorded` were pixel-identical to `completed`, and the attempt error text was dropped entirely. Status and error now reach the row and its accessible name.
- **`aria-rowcount` / `aria-rowindex` / `aria-colcount` were inert.** The stylesheet gives every table element an explicit `display`, which strips the implicit table roles those attributes require — so the virtualized position was never announced. Roles are now declared explicitly.
- **Two parsers disagreed about the same timestamp field.** An imported projection rendered durations while the chart stayed blank and every completed turn read as still running. `timelineEpochMs` is now the single parser, clamped to the `Date` range so `toISOString` cannot throw a `RangeError` out of a render.
- **A hidden pane has no scrolling box** and reports `scrollTop` 0, which clobbered the cache that is the sole record of the reading position, and anchored every off-tab prepend restore to the first entry.
- Three smaller ones: a render path that did not re-append the ledger region left a detached view still registered on `document`; the history slot re-measured its own reservation and never collapsed; the prefix-button focus latch armed across every early return and stole focus on the next repaint.

## Area

- [x] Web UI / frontend
- [x] Server / gateway / API
- [x] Tests / harness / CI

## Change Type

- [x] Bug fix
- [x] Feature

## Verification

Ran:

```text
uv run pytest                                          # full offline suite, exit 0, zero failures (green before and after the fix commit)
uv run pytest tests/test_webui_static_contract.py      # 102 assertions incl. the new ledger-row contract test
uv run pytest tests/test_action_timeline_service.py    # incl. the new branch-scoped attempts regression
uv run pre-commit run --files <changed files>          # isort / black / ruff / mypy-core all Passed, nothing rewritten
uv run python scripts/capture_response_contract.py --check   # contract up to date: 156/156 routes
uv run python scripts/check_directory_readmes.py       # complete bilingual coverage
node --check openai4s/server/webui/app.js
```

Also verified by direct repro, not by reading alone: two scripts against a real `Store` confirmed the attempt-less-group and forked-branch defects before the fix and their absence after. The branch-scoped regression test was falsified (reverted the fix, watched it fail) so it is not a vacuously-true assertion. The two changed pure functions (`timelineEpochMs`, `actionTimelineSelectionOverlaps`) were exercised through 15 node probes covering ISO strings, fractional epochs, out-of-`Date`-range values, and attempt-less groups inside and outside a selection.

Not run:

```text
node tests/browser_smoke.mjs
node tests/browser_admission_fault.mjs
node tests/browser_matrix.mjs --browser=firefox
uv run python scripts/capture_response_schemas.py --check
```

Reason:

```text
The browser gates need Playwright installed plus a daemon already serving on
127.0.0.1:8760, which was not available in this environment. They are the
gates that matter most for this diff, so CI's result on them should be
treated as the real verdict — the changed row/table markup and the scroll,
focus and role behaviour are exactly what they cover.

capture_response_schemas.py --check re-runs the whole suite under a recorder
and is known to flag machine-local drift on the /environments routes from the
local conda env list; regenerating it here would bake this machine's
environment into the frozen contract. The response *contract* gate (156/156)
was run and passes, and no response shape changed — action_timeline.py only
changes which attempt rows populate an already-existing list.
```

## Risk and Reviewer Focus

- **`openai4s/server/action_timeline.py`** is the only server change and the only one that alters what an API response contains: forked-branch requests now return their own attempts instead of an empty list. Worth confirming no consumer depended on the empty result.
- **`actionTimelineSelectionOverlaps` / `filteredActionTimelineGroups`** — the time-filter semantics changed from "is this painted?" to "when did this happen?". Groups with neither a span nor a `created_at` are still excluded.
- **Row markup** — the added status badge, ARIA roles and `—` token fallback change DOM the browser smoke test keys off. `tests/browser_smoke.mjs` asserts a specific token value on one fixture row (which does carry usage, so it is unaffected), but the browser gates were not run here.
- One existing assertion in `tests/test_webui_static_contract.py` pinned the old focus-latch literal `overview.restoreFocusAfterPrefix = true`; it now asserts the corrected conditional form, plus a negative assertion against the old one.

### Known-not-fixed (deliberate, called out rather than hidden)

Three reviewed findings were left alone because each needs a design or product decision beyond this diff:

1. Unrelated `execution_queue` / `sandbox` WS deltas still call `renderActionTimeline()`, which detaches the region and cancels an in-progress overview drag. Fixing it means restructuring which events rebuild the workbench.
2. The overview allocates one lane per group in a fixed 112px SVG, so at the default 500-group page each lane is ~0.22px. Needs time-bucketing or server-side downsampling.
3. `ACTION_TIMELINE_MAX_GROUPS` and the per-group 100-event cap were removed *deliberately* so loaded-window search works; nothing bounds client memory now. The deeper fix is server-side search (`list_groups` already builds `clauses` / `params` / `LIMIT`), which is a product call.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `app.js` is additive (10156 → 11454 lines; 73 deleted lines, 0.7% of the file, across 19 hunks). Routing, sanitizer field allowlists and the merge contract are edited in place, not replaced.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site — none added.
- [x] New dependencies, if any, are documented and justified — none added.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual verification notes — the timeline projection keeps its existing redaction boundary; no new field crosses it.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected — untouched.

---

**Note:** this branch is 15 commits behind `main`; it will need updating before the strict up-to-date check will let it merge.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a3da95ba94f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.