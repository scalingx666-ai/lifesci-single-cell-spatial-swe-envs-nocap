# Issue

**Title:** fix(ui): preserve execution history across stale reads and failed refreshes

## Description

## Summary

Execution-history responses can arrive after a newer request, snapshot, close/reopen, or session switch. Keep ownership per frame and snapshot so obsolete responses cannot replace newer cells or alter the current loading/error state. A failed refresh retains the last successful cells and retries on the next selection; error banners follow the selected frame even after switching away and back.

Replacement for #216. This preserves [dvd233](https://github.com/dvd233)'s original implementation and commit history, synchronizes with current `main`, and adds three regression fixes for cached-frame error carryover, failed-refresh retry, and active-frame error ownership. Both upstream and contribution browser scenarios are retained.

## Area

- [x] Web UI / frontend
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [x] Test / harness
- [x] Documentation

## Verification

Current head: `cb5ed516208c70bbe7529db7a96be88eebebd9b1`, synchronized with `main` at `56368bfe1a832daa87289e4fdfc42a23c5ff0c56`. The final synchronization only imports contributor documentation and avatars; application code, tests, dependencies, and build output are unchanged from the locally validated repair below. Full pre-commit, directory documentation coverage, source credential scanning, crosswalk evidence, and diff checks passed again after synchronization.

Hosted checks on this exact head completed with **34 successful and 3 conditional nightly skips**, with no failures or pending jobs (verified 2026-10-23 05:49 UTC). All required status checks passed. The [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/39906603642) passed all four Python versions (3.10, 3.12, 3.13, 3.14), Chromium/Firefox/WebKit browser jobs, frozen response shapes, route contracts, Linux sandbox/interrupt checks, packaging, lint, and the remaining PR gates. CodeQL, protocol fuzzing, and reported automated review checks also passed. No unresolved review threads; human Code Owner approval is still pending.

Local macOS validation at repair commit `64edced7cdae25fb4654200f09aa0ec7f69ccd3e`:

- Python 3.13 offline suite: **11,930 passed, 34 skipped**.
- Frontend: **1,650 tests in 147 files passed**, including 23 execution-history tests. The three added regressions were observed failing before repair.
- Chromium real-gateway workbench smoke passed, including reversed responses, a 503 followed by a real frame-button retry, preserved persisted source, close/reopen, and zero replay writes.
- Full pre-commit (including strict mypy), TypeScript, and Vite build passed; a repeated build matched committed dist.
- Offline PR harness: **38/38 passed** (12 production-backed, 26 contract-only).
- Bilingual directory docs, source credential scan, plan evidence digest, and `git diff --check` passed.

Ran:

```text
uv run --no-sync pytest -n auto --maxprocesses=4 --dist loadfile
npm test --prefix frontend
npm run build --prefix frontend
uv run --no-sync pre-commit run --all-files
uv run --no-sync python -m harness.cli run --tier pr --offline
node tests/browser_smoke.mjs
python scripts/check_directory_readmes.py
python scripts/source_secret_scan.py
python scripts/reaudit_crosswalk.py --check
git diff --exit-code -- openai4s/server/webui/dist
git diff --check origin/main...HEAD
```

The local browser run used an isolated disposable data directory and loopback daemon. Response ordering and 503 were explicitly injected; cells came from real persisted history. Linux CI and cross-engine browser results above are separate hosted evidence on the current head. Response-schema capture was not rerun locally because this diff changes no route or serializer; the hosted frozen-shape check passed.

## Risk and Reviewer Focus

Review `frontend/src/features/execution/exec.ts`, its deferred-response tests, and `executionHistoryRaceScene` in `tests/browser_smoke.mjs`. Confirm that independent frame reads still populate their own cache, stale reads fail the ownership check, retained cells do not suppress retry, and only the selected frame owns its error banner.

## Checklist

- [x] Reviewed the full diff; changes are scoped to execution-history correctness and its evidence.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor.
- [x] Compatibility/composition hotspot files are untouched by the final diff against main.
- [x] Workbench source and rebuilt committed dist land together; legacy app.js, vendor files, and captured fixtures are unchanged.
- [x] Relevant tests and browser checks are listed above; no tests were deleted or weakened.
- [x] Default offline tests need no live model, network service, cluster, credentials, or hardware.
- [x] No backend API or kernel/host-RPC protocol change; no new dependencies or hard third-party core imports.
- [x] No secrets, real credentials, private data, local absolute paths, or unpublished research content are included.
- [x] Docs match behavior and bilingual test inventories remain synchronized.

AI-assisted review, repairs, and verification with GPT-6. Code Owner approval is still required before merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56368bfe1a83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.