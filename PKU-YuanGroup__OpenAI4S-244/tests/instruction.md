# Issue

**Title:** fix(kernel): clean up recovery candidates before journaling failures

## Description

## Summary

### Introduction

A recovery candidate must remain private until validation succeeds. If the recovery journal becomes unavailable after building that candidate, `restore()` enters its failure handler and attempts another journal write before shutting the candidate down. When that terminal write fails too, cleanup is skipped. The cancellation handler has the same ordering, so an unpublished worker can outlive the failed recovery without becoming the session's active generation.

Attempt shutdown of an unpublished candidate before writing the terminal failed/cancelled event. The existing `published` guard remains in place: a candidate already adopted by the session stays alive if its subsequent journal write fails. Journal exceptions still propagate; the change does not fabricate a successful durable recovery or weaken replay safety.

The regression injects a persistent SQLite `OperationalError` at build completion or cancellation, and asserts exactly one cleanup attempt and no publication. Both cases fail on unchanged upstream with zero cleanup calls. A third case verifies that a published candidate is not shut down. Real local Python workers additionally confirm process exit on the two unpublished paths and continued execution after the published path.

Credit `JunkaiWang-TheoPhy` in the English and Chinese README contributor walls, using the existing circular-avatar generator. The avatar directory's bilingual inventories include the new PNG. GitHub's contributors API already lists this account, so future refreshes retain the entry without a manual recognition override.

## Area

- [x] Kernel / host RPC / runtime
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [x] Test / harness
- [x] Documentation

## Verification

The regression was independently run against current `main` before the fix: the build and cancellation cases fail with zero shutdown calls, while the published-candidate control passes (**2 failed, 1 passed**).

The synchronized implementation at `b70b453e` passed on macOS with Python 3.13:

```text
.venv/bin/python -m pytest tests/test_kernel_recovery.py tests/test_kernel.py tests/test_agent.py tests/test_gateway.py tests/test_session_recovery.py tests/test_recovery_recipe.py -q -ra
353 passed

.venv/bin/python -m pytest -n auto --maxprocesses=4 --dist loadfile -v -ra -o faulthandler_timeout=120
12251 passed, 43 skipped, 2 warnings in 558.83s

.venv/bin/python -m pre_commit run --all-files
All hooks passed

.venv/bin/python -m mypy
Success: no issues found in 25 source files

.venv/bin/python -m harness.cli run --tier pr --offline
38 passed, 0 failed

.venv/bin/python scripts/check_directory_readmes.py
Passed

.venv/bin/python scripts/source_secret_scan.py
Passed

node tests/browser_smoke.mjs
Passed against an isolated local daemon
```

The full-suite skips cover optional dependencies, platform-specific contracts, and an inapplicable connector fixture. The two warnings arise from tests deliberately exercising unsupported or unavailable sandbox backends. An earlier author-side macOS run encountered pipe-capacity-related failures on both base and patched code; the subsequent complete run above did not reproduce them. No sandbox/MCP tests were changed or bypassed.

Real local Python-worker fault injection passed at build, bootstrap, validation, cancellation, partial validation, and publication. Each unpublished candidate's process exited; the published candidate remained alive and executed another cell successfully. No live model calls were needed. The Chromium smoke exercised the workbench and explicit kernel recovery; the journal faults were injected separately in the worker checks.

The final `77b38a65` commit adds only contributor documentation and the avatar. All-files pre-commit and bilingual directory coverage were rerun successfully; both contributor blocks match, all local avatar links exist, and the new PNG is 256×256 RGBA with circular transparency. CI for this final head is tracked in [run 41589924504](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/41589924504).

## Risk and Reviewer Focus

Review the two exception handlers in `KernelRecoveryOrchestrator.restore` and `test_journal_failure_does_not_skip_unpublished_candidate_cleanup`. Only cleanup ordering changes; the existing best-effort `_shutdown` implementation and publication boundary are unchanged. This cannot guarantee success if a candidate's own shutdown implementation fails. A publish callback that changes ownership and then raises before returning is outside this change.

The implementation follows the existing [build-first ownership contract](https://github.com/PKU-YuanGroup/OpenAI4S/blob/ef85836a0b900799d7d478593080a84d64a86d8c/docs/architecture.md#session-kernel-ownership). No research or algorithmic novelty is claimed.

## Checklist

- [x] Focused two-file recovery fix plus the requested contributor credit in both root READMEs, one avatar, and its bilingual inventories; no unrelated formatting or rewrites.
- [x] No changes to manager/worker/gateway facades, UI bundles, fixtures or vendored files.
- [x] Regression distinguishes old and corrected implementations.
- [x] Kernel, agent and gateway checks explicitly rerun.
- [x] No live services or secrets required by the new default tests.
- [x] No tests deleted; no dependencies or core third-party imports added.
- [x] Public source and PR text contain no private data, credentials or local paths.
- [x] Journal failure remains observable; no expanded security or state-restoration claims.
- [x] Contributor entries and avatar inventories are synchronized in English and Chinese; public API shapes are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `61a5260bd775`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.