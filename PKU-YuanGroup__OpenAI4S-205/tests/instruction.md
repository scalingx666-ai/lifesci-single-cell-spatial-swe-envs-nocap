# Issue

**Title:** fix(team): send a member's own LLM key only to its provider's endpoint

## Description

## Summary

Team-mode member keys were selected by provider name alone, so an agent or Reviewer could send a cloud key to a local server or an admin-configured proxy. Credentials are now selected after the request's final provider and endpoint are known.

- A member key applies only to its registered provider endpoint over HTTPS on a non-local host. Other destinations retain their own credentials, and an unreadable member key refuses only requests where it would actually apply.
- Reviewer profiles resolve their own endpoints, including provider/environment defaults for an empty URL. Copying a keyless configuration preserves its empty key, and switching providers cannot inherit the agent's generic environment key.
- Reviewer requests apply the same member-key rule after model selection, preserving member-owned billing at eligible endpoints.
- Endpoint normalization preserves IPv6 brackets so loopback, private, and link-local IPv6 hosts cannot bypass the locality check.

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
- [x] Security-related change
- [ ] Release / packaging

## Verification

Ran on the updated branch using the repository virtual environment:

```text
uv sync --locked --extra science
python -m pytest tests/test_user_llm_key_scope.py tests/test_user_llm_keys.py tests/test_review.py tests/test_review_service.py tests/test_model_profile_identity.py tests/test_model_profile_readiness.py -n auto --maxprocesses=4 --dist loadfile
python -m pre_commit run --all-files
python scripts/check_directory_readmes.py
python scripts/source_secret_scan.py
python -m harness.cli run --tier pr --offline
python scripts/capture_response_contract.py --check
node tests/browser_team_mode.mjs
```

Focused coverage: 113 tests pass. The credential-scope module contains 33 cases; 11 of the 12 added regression cases failed before the fixes. Header-level checks cover agent and Reviewer requests without external provider calls. Pre-commit includes strict mypy. All 38 harness scenarios pass and all 215 route contracts match. The Chromium team-mode walk passes against `./start.sh` using an isolated temporary data directory and generated test accounts.

Full offline suite on Python 3.13.15:

```text
python -m pytest -n auto --maxprocesses=4 --dist loadfile --tb=short
10877 passed, 34 skipped, 2 warnings in 513.83s
```

The completed local suite ran outside the command sandbox so macOS process controls, R file descriptors, and Seatbelt tests could execute. An earlier sandbox-restricted attempt hit those OS restrictions and was interrupted; it is not counted as a passing run.

GitHub validation at `2dc4d0229f098c65c285d7aa652e986070e706c3`: **34 successful checks, no failed or pending checks**, plus four neutral/skipped checks (Bugbot and the three scheduled-only jobs). The [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/36993989086) passed the Python 3.10/3.12/3.13/3.14 suites, frozen response shapes, Chromium/Firefox/WebKit browser gates, team mode, packaging, container startup, and both Linux sandbox jobs. The automated security review also passed.

Not run locally: the separate frozen response-shape capture, Linux-only sandbox smokes, Docker build, and other browser engines. These run separately in CI; no live provider calls or real credentials were used for validation.

## Risk and Reviewer Focus

- `openai4s/server/model_profiles.py`: member-key endpoint and locality gate before reading any member secret.
- `openai4s/server/reviews.py`: complete Reviewer destination resolution and credential assignment after `LLMConfig.__post_init__`.
- `openai4s/server/gateway.py`: surgical wiring changes that defer member-key selection until the Reviewer's endpoint is final.
- `openai4s/endpoint_identity.py`: preservation of IPv6 URL brackets during normalization.
- `tests/test_user_llm_key_scope.py`: local/proxy/default endpoint transitions, IPv6, environment fallback, unreadable member keys, and transport headers. The stubbed transport test is marked `stubbed_backend` to keep fabricated data out of response captures.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`.
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
      weights, or local absolute paths are included. (Test keys are synthetic.)
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate. (`docs/security.md`, team-server EN/ZH, `docs/webapp-api.md`, plan deviation log, tests README EN/ZH.)
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected. (Root READMEs not affected.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b7aa70d60c1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.