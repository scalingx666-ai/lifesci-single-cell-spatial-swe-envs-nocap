# Issue

**Title:** fix(server): report folder_id on GET /frames list rows

## Description

## Summary

Sessions moved into a folder never appeared inside it in the sidebar.

`GET /frames` builds its rows with `store.browse_frames(...)`, whose explicit
column list omitted `folder_id`. `_frame_json` reads the key with `.get`, so the
omission was silent: every list row answered `folder_id: null`, while
`POST /frames/{id}/folder` had succeeded, SQLite held the right value and
`GET /frames/{id}` (which uses `SELECT *`) reported it. The sidebar groups by
that field (`features/sessions/load.ts`), so a folder always counted 0 and its
sessions fell into the date buckets.

- **Fix:** add `folder_id` to the `browse_frames` SELECT
  (`openai4s/storage/frames.py`). The other callers (`server/attention.py`,
  `server/global_views.py`, the example-session seeding in `gateway.py`) read
  rows by name, so an extra column is inert there. The agent-facing
  `host.frames` browse mode gains `folder_id`, matching what its detail mode
  already returned. `docs/webapp-api.md` already documented `folder_id` on list
  rows, so the docs were already describing the fixed behavior.
- **Regression test:** new `tests/test_session_list_folder_id.py`, unmarked so
  the schema capture observes it:
  - The repository row carries the stored folder.
  - Over a real socket, a moved session's list row carries its folder and a
    moved-out one returns to null.
  - A list row reports every field the detail route reports, identically.
    The fixture sets every root field first, because with nulls on both sides
    the parity check was vacuous. Dropping `model`, `task_summary`,
    `input_tokens` or `updated_at` from the SELECT now fails it.
- **Frozen shapes:** `docs/response-schemas.json` was regenerated.
  - `GET /frames` and `GET /frames/{id}` now record `folder_id` (and `name`,
    `model`, `task_summary`, token counts) as observed with values instead of
    null-only.
  - `PATCH /frames/{id}` now records the frame it returns.
  - The capture also picked up `PUT /models/default [error]`. This is a real
    404 from an unmarked test that landed after the previous capture.
  - `GET /compute/remote [ok]` is kept at its committed shape: its `hosts` come
    from the capturing machine's `~/.ssh/config`, so a local narrowing is not a
    contract change.
- **`EMPTY_ACK`:** the frame catch-all `/frames/([^/]+)(?:/.*)?` is retired
  from the exemption list in `tests/test_response_contract_coverage.py`. Its
  bare `{}` came only from the contract probe patching a nonexistent frame. Now
  that a real session is patched, no `{}`-only schema remains under that route,
  and `test_an_empty_acknowledgement_is_still_an_observed_one` correctly
  flagged the stale entry.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [x] Server / gateway / API
- [x] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [ ] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [x] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Validated the synchronized PR head `2a5e37be` against `main` at `915d2675`
(macOS, Python 3.13, locked `science` and `chemistry` extras):

```text
python -m pytest tests/test_session_list_folder_id.py tests/test_frame_repository.py \
  tests/test_frame_pagination.py tests/test_session_sidebar_scope.py \
  tests/test_session_and_message_paging.py tests/test_response_contract_coverage.py
# 52 passed

python scripts/capture_response_schemas.py --check
# Full offline suite: 10,887 passed, 26 skipped.
# 1,185 route/status shapes; 215/215 routes; no breaking changes.

python scripts/capture_response_contract.py --check  # 215/215 routes, up to date
python scripts/check_directory_readmes.py           # complete bilingual coverage
python scripts/source_secret_scan.py                # passed, 4,082 files
python -m harness.cli run --tier pr --offline        # 38/38 passed
pre-commit run --all-files                          # all hooks passed, including mypy
```

Regression proof: temporarily removing `folder_id` from the SELECT makes both
folder regression tests fail; the fix was restored before the full suite.
The capture reported only a non-breaking, machine-dependent difference on
`GET /compute/remote`; that unrelated frozen shape was preserved.

Real Chromium against an isolated `./start.sh --no-browser` daemon:

- Move a session into a folder through the sidebar menu: the folder count and
  the nested session update without reload; the list API returns its folder ID.
- Reload: folder membership persists.
- Remove the session through the sidebar menu: the count returns to zero and
  the session returns to its date group without reload.
- Delete a populated folder through its menu: both sessions remain visible and
  both list rows report `folder_id: null`.
- No browser page errors.

GitHub checks on this head: **34 successful**, **zero pending or failing**,
three schedule-only jobs skipped, and Cursor Bugbot neutral because its usage
limit prevented the run. [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/36998240906).

The Python 3.10/3.12/3.13/3.14 suites, frozen schemas, browser engines, container
build, Linux sandbox checks, and all required merge checks passed. Python 3.14
passed on a single-job rerun: **10,828 passed, 85 skipped**. Its first attempt
was manually cancelled before completion; no test failure was recorded before
cancellation. GitHub reports `CLEAN` and `MERGEABLE` for this head.

## Risk and Reviewer Focus

- `openai4s/storage/frames.py`: the single-column SELECT change.
- `host.frames` browse output gains a `folder_id` key (additive, agent-facing).
- `docs/response-schemas.json`: please confirm that the four changed routes
  are the intended ones.
- `tests/test_response_contract_coverage.py`: the one `EMPTY_ACK` entry
  removed.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. (None touched.)
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`)
      and `openai4s/server/webui/dist/` was rebuilt and committed with the
      source. (No workbench changes.)
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site.
- [x] New dependencies, if any, are documented and justified. (None.)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes. (Not security-related.)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected. (`tests/README.md` and `tests/README_zh.md` each gained the
      new row.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Single additive column in a read query plus contract/test updates; behavior aligns list API with existing detail and documented shapes.
>
> **Overview**
> **Fixes sidebar folder grouping** by including `folder_id` in the `browse_frames` SELECT in `openai4s/storage/frames.py`. `GET /frames` used that query while detail used `SELECT *`, so list rows always serialized as `folder_id: null` even after a successful move; the sidebar groups on that field.
>
> Adds **`tests/test_session_list_folder_id.py`** (repository + real-socket HTTP) asserting list rows match detail for sessions in folders, and updates **`docs/response-schemas.json`** so frame list/detail shapes allow non-null `folder_id`, `name`, `model`, tokens, etc., documents **`PATCH /frames/{id}`** returning the updated frame, and records **`PUT /models/default [error]`**. Drops the stale **`EMPTY_ACK`** catch-all for frames in **`test_response_contract_coverage.py`** because patching a real session no longer yields an empty `{}`.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 2a5e37be61bbec4e0e6c4de318b09b8a188b23da. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `915d2675f8a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.