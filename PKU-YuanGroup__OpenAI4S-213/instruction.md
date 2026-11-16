# Issue

**Title:** test(frontend): make the workbench gates pass on a Windows checkout

## Description

## Summary

Git for Windows CRLF checkouts and non-English system locales made the documented frontend gates fail on clean source. This PR fixes those failures and the Settings lazy-mount test race:

- Remove the unused extractor shebang that breaks Vitest collection with CRLF; normalize checkout line endings when comparing generated dictionaries.
- Pin English in tests that assert English UI copy, then restore the system language.
- Normalize HTML before Vite transforms module-script lines, so LF and CRLF inputs produce identical committed output. Keep output validation and README generation exclusive to builds, including isolated Vite tests.
- Cover LF/CRLF build equality, continued rejection of inline scripts, and preservation of existing output when a test server closes.
- Await the shared Settings mount promise before checking the window export. The previous one-second poll failed on slow imports even when the UI loaded correctly; the original open/tab assertions remain.

The branch includes current `main` (`0e04ff63`). Production workbench assets remain byte-identical after rebuilding.

## Area

- [x] Web UI / frontend
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

Local validation on macOS (Node 24.21.0, Python 3.13.15):

```text
npm test --prefix frontend
# 138 files, 1408 tests passed

# CRLF scratch checkout + navigator.languages = ["zh-CN", "zh"]
npm test --prefix frontend
# 138 files, 1408 tests passed

# Inject a 1500 ms delay into the real Settings module import in a scratch copy:
# original assertion fails after ~1000 ms; repaired test passes (10/10 in the file).
# Counterproof: removing the window open call still fails the repaired assertion.

node frontend/src/i18n/extract-i18n.mjs --check
# 1213/1213 dictionary entries match, in LF and CRLF copies

npm run build --prefix frontend
git diff --exit-code -- openai4s/server/webui/dist
# No drift; every output file also matches the CRLF source build byte-for-byte.

uv run pytest -n auto --maxprocesses=4 --dist loadfile --tb=short
# 11382 passed, 34 skipped; Python code unchanged by the final test-only fix.

uv run pre-commit run --all-files
# All hooks passed, including strict mypy.

python scripts/check_directory_readmes.py
# Complete bilingual coverage.
python -m harness.cli run --tier pr --offline
# 38 passed, 0 failed.
python scripts/source_secret_scan.py
# Passed, 4096 files.

node tests/browser_smoke.mjs
# Passed against an isolated local daemon: real Chromium workbench E2E.
```

The complete Python run and Chromium launch used normal macOS process permissions: the restricted command sandbox blocks nested Seatbelt self-tests and Chromium Mach ports. No production Python or UI code changed in the final Settings-test fix, and the final frontend suite, build, and complete pre-commit hooks were rerun.

Not run locally: native Windows frontend rerun and nightly-only jobs. CRLF plus Chinese locale was simulated locally; native Windows launcher coverage and Linux checks run in GitHub Actions.

Hosted validation for `e99f765a`: **27 successful checks**, with 3 nightly-only jobs skipped by design. [CI](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38227260774) and [protocol fuzzing](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/38227260718) both passed. This includes Python 3.10/3.12/3.13/3.14, frozen response shapes, and Chromium/Firefox/WebKit workbench E2E.

## Risk and Reviewer Focus

- `frontend/vite.config.ts`: normalize input before Vite transforms it; retain CSP validation for builds and avoid output writes during test/dev-server shutdown.
- `frontend/src/i18n/extract-i18n.mjs`: only checkout line endings are ignored; dictionary content differences still fail.
- Locale-sensitive tests retain their original assertions. The Settings test now waits on its real mount promise instead of a one-second polling deadline.
- No dependency or production UI behavior changes; rebuilt `openai4s/server/webui/dist/` is unchanged.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: none of the listed hotspots changed.
- [x] Workbench changes were made in `frontend/` (not legacy `app.js`) and `openai4s/server/webui/dist/` was rebuilt and committed with the source. (Build run; dist byte-identical, nothing to commit.)
- [x] `openai4s/server/webui/vendor/` and `tests/fixtures/` were not reformatted.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.
- [x] Kernel / host-RPC / gateway changes include focused contract coverage or a documented smoke test. (N/A — frontend test tooling only.)

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
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are affected. (No translated sections touched.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0e04ff6308f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.