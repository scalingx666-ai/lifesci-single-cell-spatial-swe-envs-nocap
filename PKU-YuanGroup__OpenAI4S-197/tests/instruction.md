# Issue

**Title:** test: stabilize mobile drawer and shadow idle checks

## Description

## Summary

Two timing races could fail otherwise healthy CI runs:

- At 375x812, the open mobile drawer covers the full-screen scrim's center. A default Playwright click could succeed during the slide-in animation and time out once the drawer settled. The browser smoke now waits for the drawer to settle and clicks the exposed scrim strip. A strip narrower than 16px fails with a geometry error, and the existing collapsed/reopen assertions still verify the actual click handler.
- The task-mode shadow's `wait_idle()` could return between the last queue dequeue and the worker's in-flight registration. Callers could then observe only 35 of 36 backend calls. The bounded wait now uses the queue's unfinished-task condition, which remains accurate after dequeue and counter reset. Two deterministic regression cases cover these gaps.

The notebook-export evidence digest in `docs/plan-crosswalk.json` matches the retained browser assertions. The branch includes current `main` (`9de3f55d`).

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [ ] Server / gateway / API
- [ ] Store / provenance / artifacts
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

Current head: `7dc54955`. Local validation uses macOS, Python 3.13.15 (plus a focused Python 3.10.21 run), Node 24.21.0, and locked Playwright 1.63.0.

```text
# Installed with uv sync --locked --extra science --extra chemistry
uv run --no-sync pytest -n auto --maxprocesses=4 --dist loadfile
  -> 10,834 passed, 26 skipped, 2 expected platform-sandbox warnings (510.64s)
uv run --no-sync pytest tests/test_judgment_task_mode_shadow.py tests/test_real_data_dir_guard.py -o addopts='' -q
  -> 27 passed
python3.10 -m pytest tests/test_judgment_task_mode_shadow.py -o addopts='' -q
  -> 15 passed
uv run --no-sync pre-commit run --all-files
  -> all hooks passed, including strict mypy
uv run --no-sync python scripts/reaudit_crosswalk.py --check
  -> 47 closed rows up to date
node --check tests/browser_smoke.mjs
  -> passed
node tests/browser_smoke.mjs
  -> OpenAI4S browser smoke passed
uv run --no-sync python -m harness.cli run --tier pr --offline
  -> 38/38 passed (26 contract-only, 12 production-backed)
uv run --no-sync python scripts/check_directory_readmes.py
  -> 171 maintained directories, 1,744 direct files/assets; complete bilingual coverage
uv run --no-sync python scripts/source_secret_scan.py
  -> passed (4,080 files)
```

Both new unfinished-job cases were run before the idle-wait fix and failed, then passed after the fix. The full offline suite above passed on the final committed source and isolated regression tests.

The browser ran against a disposable data directory and credential-free daemon started through `./start.sh --no-browser`, with `OPENAI4S_NOTEBOOK_REPL=1`, `OPENAI4S_KERNEL_SANDBOX=off`, and `OPENAI4S_SECRET_STORE=plaintext`. A temporary probe executed the exact drawer-closure block against the real 375x812 workbench:

| Motion preference | Old center click after drawer settles | PR closure | Drawer covers whole scrim |
| --- | --- | --- | --- |
| no-preference | pointer-interception timeout reproduced | 8/8 passed | clear geometry error |
| reduce | pointer-interception timeout reproduced | 8/8 passed | clear geometry error |

The browser, harness, and directory-documentation results above were obtained before the additional idle-wait helper fix; the browser test and UI files are identical in the current head. [Fresh CI on the final code](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/36979057059) completed successfully, including the Linux-only checks, Chromium/Firefox/WebKit browser harnesses, response contracts, and Python 3.10/3.12/3.13/3.14 matrix. All 34 PR checks passed; three nightly-only checks were skipped. Code-owner approval remains outstanding.

## Risk and Reviewer Focus

- The scrim position is relative to its bounding box. Playwright still checks the real hit target; no forced click bypasses interception. The settle wait uses `locator.boundingBox()` because the workbench CSP blocks `page.waitForFunction`.
- `wait_idle()` retains its timeout and boolean result. Queue completion includes work already removed from the queue and remains valid when test reset clears diagnostic counters. The worker execution, submission, and task-mode selection paths are not modified.
- The two new tests exercise the dequeue gap deterministically in fresh Python processes, including a reset before completion, without swapping queues underneath persistent suite workers. Existing real-worker tests continue to cover backend calls, audit completion, and queue saturation.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. (not touched)
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`)
      and `openai4s/server/webui/dist/` was rebuilt and committed with the
      source. (no workbench change)
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not
      reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware,
      or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or
      a documented smoke test. (no such change)

### Core Dependency Policy

- [x] No hard third-party import was added to the core engine, LLM client, or
      stdlib web server.
- [x] Optional science imports are guarded by `try/except ImportError` at every
      in-tree use site.
- [x] New dependencies, if any, are documented and justified. (none)

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model
      weights, or local absolute paths are included.
- [x] No unpublished research roadmap, internal assignment, benchmark detail,
      or unreleased experimental result is disclosed.
- [x] Security-sensitive changes include appropriate synthetic tests or manual
      verification notes. (not security-sensitive)
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate. (no user-facing change)
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9de3f55d5351`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.