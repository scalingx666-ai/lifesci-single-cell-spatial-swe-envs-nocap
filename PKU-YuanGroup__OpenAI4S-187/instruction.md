# Issue

**Title:** fix(diagnostics): say how recent turns ended, the version, and WSL

## Description

## Summary

A WSL user on 0.3.0 attached an `openai4s diagnostics` bundle to a "已停止重复动作" (no-progress stop) report. The bundle could not explain the stop. The logs are reduced to line-class counts, which is correct. But `report.json` lacked three facts:

1. **The openai4s version.** `_version()` read only `importlib.metadata`, and without a dist-info it answered `"unknown"`. `_v_version` correctly dropped that value, so the report showed only `environment.fields_omitted: 1`. The version now falls back to `openai4s.__version__` first.
2. **WSL.** The release `6.6.87.2-microsoft-standard-WSL2` is reduced to `6.6.87`, which cannot be told apart from any other Linux host. The new `environment.wsl` boolean is read from the release or `/proc/version`. Neither string leaves the machine.
3. **The stop itself.** The new `agent_turns` section counts the Action Ledger terminal `reason`, the no-progress `progress_reason`, and the wire family of each turn's provider. It covers the last 20 top-level turns and also gives the latest turn's codes:

   ```json
   "agent_turns": {"status": "ok", "window": 20, "terminals": 1,
     "reasons": {"no_progress": 1}, "progress_reasons": {"consecutive_malformed": 1},
     "wires": {"openai": 1},
     "latest": {"reason": "no_progress", "progress_reason": "consecutive_malformed", "wire": "openai"}}
   ```

   That example is real `openai4s diagnostics` output, run against a database left by a reproduced 0.3.0 no-progress stop.

Design points:
- **Read-only.** The ledger is read through the same `mode=ro` handle the schema probe uses, so it never writes. A hot journal is reported as `interrupted_write` and left for the read-write open that replays it. A missing database reports `no_database`, a database with no ledger reports `no_ledger`, and a corrupt one reports `unavailable` with its `error_type`.
- **Top-level turns only.** Delegated children record their own terminals under their own frame, so they are excluded (`frames.parent_id IS NULL`). Otherwise one fan-out could push the user's own turns out of the window.
- **Closed sets only.** Only codes from sets written down in `diagnostics.py` leave the machine. Anything else is counted as `other` or `unknown`. The report schema admits only those sets, and a lying `str` subclass is dropped. Provider ids and model names are never reported, because an operator names both. The wire family is resolved through the provider registry.
- **Drift guard.** A test reads every stop reason the source can record out of the code and requires the set to contain it. It finds 15: the Engine's stops, `plan`, the gateway's fallbacks, the four model-call failures a turn can be continued from, and the Auto Mode budget refusals. A reason added later fails CI instead of arriving in bundles as `other`.

`GET /diagnostics/status` returns `environment.wsl` too. `docs/response-schemas.json` was recaptured, and exactly one entry changed: that route gained a required boolean. `docs/security.md` describes the new fields and their rules.

## Area

- [ ] Web UI / frontend
- [ ] Agent / loop / delegation
- [ ] Kernel / host RPC / runtime
- [x] Server / gateway / API
- [ ] Store / provenance / artifacts
- [ ] Skills / science runtime
- [ ] Compute / remote execution
- [x] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Docs

## Change Type

- [x] Bug fix
- [x] Feature
- [ ] Refactor
- [ ] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
uv run pytest -q tests/test_diagnostics.py tests/test_diagnostic_archive_boundary.py \
  tests/test_diagnostics_routes.py tests/test_doctor.py
uv run python scripts/capture_response_schemas.py           # rewrote docs/response-schemas.json;
                                                             # the only changed entry: GET /diagnostics/status [ok]
uv run python scripts/capture_response_schemas.py --check   # full suite: 10612 passed, 34 skipped;
                                                             # no breaking change; 215/215 routes exercised
uv run python scripts/capture_response_contract.py --check  # contract up to date: 215/215 routes
uv run pre-commit run --all-files                            # all hooks passed
uv run mypy                                                  # Success: no issues found in 25 source files
uv run python3 -m harness.cli run --tier pr --offline        # 38/38 passed
uv run python scripts/check_directory_readmes.py             # complete bilingual coverage
python scripts/source_secret_scan.py                         # passed

Mutation check: each of 8 reverts turns at least one new test red. The reverts
are: the version fallback, the section in the bundle, the section in the schema,
`wsl` in the schema, the WSL probe, counting delegated children, passing a raw
reason through, and the hot-journal mapping.

End to end: `openai4s diagnostics` on a database left by a reproduced 0.3.0
no-progress stop prints the section above. The database's SHA-256 is identical
before and after.
```

Not run:

```text
browser E2E (node tests/browser_*.mjs)
```

Reason:

```text
No workbench change. The Diagnostics tab renders only the `security` posture
from GET /diagnostics/status, so the new `environment.wsl` key is not displayed.
```

## Risk and Reviewer Focus

- `docs/response-schemas.json`: `GET /diagnostics/status [ok]` gains a required `environment.wsl: boolean`. The change is additive, and no other entry moved in the recapture.
- The Web bundle is built inside the daemon, so the ledger read opens a second, read-only SQLite handle in the daemon process, as `preflight_schema` already does there. If the database is locked, the read waits out SQLite's default timeout and then reports `unavailable`. It does not fail the bundle.
- The terminal query filters `action_groups` on `kind = 'terminal'`, which has no index, so the whole table is scanned. Only the small terminal rows are read in full. This is a one-off, on-demand read.
- `_TURN_REASONS`, `_PROGRESS_REASONS` and `_WIRE_FAMILIES` are closed sets in `openai4s/diagnostics.py`. `tests/test_diagnostics.py` pins them to their sources: the AST scan, `PROGRESS_REASONS`, and `SUPPORTED_WIRES`.
- A custom provider resolves to a wire family only if the process that builds the bundle has it registered. Otherwise it is reported as `unknown`.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `worker.py`, `manager.py`. (None touched.)
- [ ] Workbench changes were made in `frontend/` (not legacy `app.js`)
      and `openai4s/server/webui/dist/` was rebuilt and committed with the
      source. `OPENAI4S_WEBUI=legacy` is an escape hatch, not a place to add
      features. (N/A: no workbench change.)
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
      verification notes.
- [x] Docs do not overstate isolation, sandboxing, privacy, or security
      guarantees.

### Docs

- [x] Docs match actual code behavior.
- [x] User-facing behavior changes are reflected in docs or release notes where
      appropriate.
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected. (Not affected.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Medium Risk**
> Adds a read-only ledger query in the daemon when building diagnostics (second SQLite handle, possible lock wait) and expands shareable **`report.json`** with new closed-set fields—bounded by existing archive sanitization but touching support-facing data paths.
>
> **Overview**
> Diagnostic bundles and **`GET /diagnostics/status`** now carry facts support was missing when users reported early stops (e.g. no-progress on WSL).
>
> **Environment:** **`openai4s`** falls back to **`openai4s.__version__`** when installer metadata is absent, so **`report.json`** no longer omits the version as **`fields_omitted`**. A required **`environment.wsl`** boolean records WSL without shipping **`microsoft`** / WSL release strings (release stays numeric-only).
>
> **Turn stops:** **`report.json`** gains **`agent_turns`**, built by **`turn_stop_report()`** via a read-only SQLite open on the Action Ledger (same posture as the schema probe—no upgrade, **`interrupted_write`** when a hot journal exists). It summarizes the last 20 **top-level** terminals: closed-set **`reason`**, **`progress_reason`**, and provider **wire** counts plus **`latest`**, with unknown codes mapped to **`other`**/**`unknown`** and no provider/model/prompt text. **`docs/security.md`** and **`docs/response-schemas.json`** reflect the schema; tests guard archive boundaries and stop-reason drift.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 572acaa587af781b90c3ef2227be5036c5ddacc9. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `829b8023f7a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.