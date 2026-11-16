# Issue

**Title:** fix(server): answer an edit of an unknown project with 404

## Description

## Summary

`PUT` and `PATCH /api/v1/projects/{pid}` returned `200 {}` when the project did not exist, so the workbench closed its edit modal as though the save had succeeded. The handler now returns `404 project not found` before writing and checks again after the update in case the project was deleted concurrently. The error envelope matches team-mode missing and inaccessible projects (INV-13).

Successful edits and empty edits of existing projects still return full project JSON. `GET /projects/{pid}` retains its documented compatibility behavior. The frozen schemas and API documentation record the mutation's new error response.

The branch includes current `main` and resolves the overlap with PR #202: the session GET compatibility exemption remains, and the obsolete project-update exemption is removed. Regression coverage exercises both verbs across solo, member, non-participant and admin callers, plus deletion before and after the real database update. Fault-injection cases carry `stubbed_backend` and cannot contribute captured schemas.

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
- [x] Test / harness
- [x] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Local checks use scratch application data and the locked `science` and `chemistry` extras.

```text
.venv/bin/python -m pytest tests/test_project_patch_unknown_id.py tests/test_frame_patch_unknown_id.py tests/test_response_contract_coverage.py
  23 passed
.venv/bin/python scripts/capture_response_schemas.py --check
  10,898 passed, 26 skipped; 1,188 shapes; 215/215 routes; no breaking drift
  Only GET /compute/remote reported a machine-dependent additive shape.
.venv/bin/python scripts/capture_response_contract.py --check
  215/215 routes; contract up to date
.venv/bin/python -m harness.cli run --tier pr --offline
  38 passed (26 contract-only, 12 production-backed)
.venv/bin/pre-commit run --all-files
  all hooks passed, including strict mypy and CSS tokens
.venv/bin/python scripts/check_directory_readmes.py
  complete bilingual coverage
.venv/bin/python scripts/source_secret_scan.py
  passed
node tests/browser_smoke.mjs
  passed against the isolated loopback daemon
```

A separate Chromium check against `./start.sh --no-browser` verified that a successful save closes the project modal; deleting a project while its edit modal is open makes Save return 404, displays the error, retains the entered text, and keeps the modal open. It also verified missing-project PUT returns 404 and GET still returns `200 {}`.

Not run locally: container, hosted Linux bubblewrap, Firefox/WebKit and the remaining browser suites. These are separate CI jobs; no frontend, kernel, sandbox or packaging code changes in this PR.

Hosted validation for head `5b0150780bf1bcd3a1dbebe2341c8f1367d5993a`: **34 checks passed, 3 scheduled nightly checks skipped, none failed or pending**. [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/37046954805) passed, including Python 3.10/3.12/3.13/3.14, frozen schemas, Chromium/Firefox/WebKit, container and Linux bubblewrap checks. The pushed tree is identical to the locally tested tree. Current `main` (`59cd608d`) is included, no review threads are unresolved, and code-owner approval remains outstanding.

## Risk and Reviewer Focus

- The externally visible behavior change is limited to editing a missing project: 404 replaces silent `200 {}`. Existing workbench error handling already retains the failed edit.
- `gateway.py` is changed surgically in the project PUT/PATCH branch. GET compatibility and team authorization remain unchanged.
- The post-update read is covered for deletion on either side of the database write. This does not promise an atomic update-and-response transaction.
- Code-owner approval remains required by repository policy before merge.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `59cd608db328`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.