# Issue

**Title:** fix(server): return 400 for invalid project-view limits

## Description

## Summary

`GET /projects/{pid}/action-timeline` and `GET /projects/{pid}/lineage` returned 500 for invalid `limit` query values. Both routes now return 400 `invalid_limit`: non-integers report `limit must be an integer`, while zero and negative integers report `limit must be a positive integer`. Missing/blank limits retain their defaults, and positive values retain the service's upper bounds.

Real HTTP regressions verify the complete error envelope, limits applied to stored Timeline/Artifact records, authentication before validation, and identical 404 responses for inaccessible and missing projects. The branch includes current `main` (`aaa66537`), preserving the contributor's original commits.

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
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
python -m pytest tests/test_project_view_routes.py tests/test_global_research_views.py
# 16 passed; real HTTP, Store, view services, and team authorization.

# Counterproof before the positive-range fix: both endpoints with 0 and -1
# failed their 400 assertions, returning 500 internal_error (4 failures).

python -m pre_commit run --all-files
# Passed: formatting, lint, mypy, and hygiene; rerun after Black formatted tests.

python scripts/check_directory_readmes.py
# Complete bilingual coverage: 171 directories, 1761 direct files/assets.
python scripts/source_secret_scan.py
# Passed: 4097 files.
python -m harness.cli run --tier pr --offline
# 38 passed (26 contract-only, 12 production-backed).
python scripts/capture_response_contract.py --check
# 215/215 routes, up to date.

node tests/browser_smoke.mjs
# Passed against an isolated daemon with the CI Notebook/kernel settings.
# Additional Chromium same-origin fetches: 14/14 passed across both endpoints,
# covering non-integers, zero, negative, positive, large, and blank limits.

python scripts/capture_response_schemas.py --check
# Local macOS / CPython 3.10 full suite: 11390 passed, 37 skipped, 3 failed.
# The 3 BioProBench PQA failures are SciPy 1.15.3 _spropack Mach-O load errors.
# The exact 3 failures reproduce on unmodified main aaa66537 using the same
# interpreter. This local schema-check invocation therefore exits before
# comparing the capture; it is not claimed as a local pass.
```

Hosted validation at `ba856f41`: **27 checks passed; 3 nightly-only checks skipped**. This includes offline suites on Python 3.10/3.12/3.13/3.14, frozen response shapes, response contracts, all three browser engines, Stage 0/team browser tests, packaging, container, sandbox, lint, and type checks. [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38234281815).

No review threads remain unresolved. A Code Owner approval is still required by the repository ruleset before merge; this PR has not been merged.

The initial terminal-sandbox suite was interrupted after process-control tests stalled near completion. The full result above is from the subsequent run with normal OS capabilities. No production source was changed to work around either environment limitation.

Not run: live LLM, GPU, SSH, or lab-hardware tests; this change requires none.

## Risk and Reviewer Focus

- `openai4s/server/gateway.py`: surgical parsing and positive-range guards before either view service executes. Authentication and project visibility still run first; service algorithms and valid-request behavior are unchanged.
- `tests/test_project_view_routes.py`: real socket requests and populated Store records replace direct handler-only checks. Regressions cover complete 400 envelopes, valid limits/defaults, and refusal ordering without backend stubs.
- `docs/webapp-api.md` and the bilingual test indexes describe the accepted range and errors. Existing response envelopes remain compatible.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py` (integer parsing and positive-range guards).
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`) — no UI change; dist untouched.
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test.

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every in-tree use site. (No imports added.)
- [x] New dependencies, if any, are documented and justified. (None.)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail, or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual verification notes. (Not security-sensitive.)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected. (`tests/README.md` + `tests/README_zh.md`.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aaa66537bf9e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.