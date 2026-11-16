# Issue

**Title:** fix(server): answer PATCH of an unknown session with 404

## Description

## Summary

Renaming a deleted or unknown session previously returned `200 {}` and emitted a `frame_update`, so the workbench could report a rename as saved even though no row existed. `PATCH /api/v1/frames/{fid}` now returns `404 session not found` for a missing row, using the same error as the team visibility guard.

The handler checks existence before the write and again before broadcasting success. Deletion immediately before or after the metadata write therefore returns 404 without a misleading success event. Normal renames and empty-body patches still return the complete frame; the documented single-user GET compatibility response remains `{}`.

- Real-socket tests cover successful/empty patches, unknown IDs, and identical missing/not-visible refusals in team mode. Two additional deterministic deletion cases reproduce the premature broadcast on the previous code and pass with the fix; they carry `stubbed_backend` to exclude fault injection from response capture.
- Response schemas and API documentation reflect the PATCH error and real-frame success shapes. The existing machine-dependent remote-host schema is preserved.
- Includes current `main` (`9b7a12b8`); the deletion-race fix is isolated in `6e09263e`.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [x] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [ ] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [ ] Feature
- [ ] Refactor
- [ ] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran on the integrated code:

```text
.venv/bin/python -m pytest tests/test_frame_patch_unknown_id.py tests/test_gateway.py tests/test_agent.py tests/test_kernel.py -n auto --maxprocesses=4 --dist loadfile
  282 passed
.venv/bin/python scripts/capture_response_schemas.py
  10883 passed, 34 skipped; 1186 response shapes; 215/215 routes
.venv/bin/python scripts/capture_response_contract.py --check
  contract up to date: 215/215 routes
.venv/bin/pre-commit run --all-files
  all hooks passed, including strict mypy
.venv/bin/python scripts/check_directory_readmes.py
  complete bilingual coverage
.venv/bin/python scripts/source_secret_scan.py
  passed
.venv/bin/python -m harness.cli run --tier pr --offline
  38/38 passed
node tests/browser_smoke.mjs
  passed against an isolated daemon started with ./start.sh
```

A separate real Chromium check used the workbench title input: a normal rename persisted, then deletion followed by another rename returned 404, restored the prior title, and displayed the failure hint. GET of the deleted session remained `{}`.

The first full-suite attempt ran inside a restricted terminal sandbox, which blocked process inspection, Seatbelt, and R protocol-file access; it was interrupted and superseded by the passing unrestricted offline run above. No tests were disabled to obtain the passing result.

The final local `capture_response_schemas.py --check` also passed: 10,883 passed, 34 skipped, 215/215 routes, and no breaking response-shape change. Its only additive drift was the machine-dependent `GET /compute/remote` host list, whose existing frozen schema was preserved.

: **34 passed, 3 configured nightly checks skipped, none failed or pending**. This includes Python 3.10/3.12/3.13/3.14, frozen response shapes, route contracts, Chromium/Firefox/WebKit, Linux interrupt and filesystem/egress sandbox checks, container/package gates, lint, and security checks.

The PR is conflict-free (`MERGEABLE`) and includes current `main`. GitHub still reports `BLOCKED`: no approving code-owner review has been recorded, and the existing reviewer requests remain open. The repository's review policy still requires that approval; this PR has not been merged.

## Risk and Reviewer Focus

- The gateway change is confined to the frame PATCH arm. Review the existence checks and the ordering of the post-write read before `hub.broadcast`.
- Callers relying on PATCH of an unknown ID returning 200 now receive 404. The actual workbench failure path has been verified in Chromium.
- GET compatibility and team missing/not-visible error equivalence are covered explicitly.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`.
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`)
      and `openai4s/server/webui/dist/` was rebuilt and committed with the
      source. `OPENAI4S_WEBUI=legacy` is an escape hatch, not a place to add
      features. (No workbench changes.)
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
- [x] New dependencies, if any, are documented and justified.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b7a12b834a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.