# Issue

**Title:** fix(agent): stop no_progress from ending turns two steps in

## Description

## Summary

A user on 0.3.0 under WSL reported that every turn stopped with "已停止重复动作" ("Stopped repeating actions") after two or three steps. It happened with GLM 5.3 Flash and with Opus 4.6. The no-progress circuit was working as designed. Three kinds of input tripped it early, and none of them depend on the model. All three reproduce against the released 0.3.0 Web daemon and against current `main`, driven by a scripted OpenAI-compatible relay:

1. **A native call displaced a code cell** (`same_action`, 3 steps). When one reply carries native tool calls *and* a ```python cell, `route_action` runs only the calls. The model got back only what the calls returned, for example `write_file`'s byte count. Nothing told it the cell never ran, so it sent the same pair again, and the circuit stopped the turn on the third identical write. The engine now appends a note to the last tool result. The note says the cell did not run and asks the model to send it as the only action of its next reply. The note is recorded like any other result, so restored history reads the same words. A model that ignores the note is still stopped by the circuit.
2. **A relay sends `arguments: ""` for a parameterless tool** (`consecutive_malformed`, 2 steps). `json.loads("")` made it a malformed call that never ran. `_parse_tool_arguments` now reads an empty, whitespace-only or null argument string as `{}` on every wire, and replays it as `"{}"`. The Anthropic adapter already read its own empty input as `{}`.
3. **A relay omits `tool_calls[].index` in SSE** (`consecutive_malformed`, 2 steps). Every fragment without an index was read as index 0. Parallel calls merged into one malformed call: the arguments became `{"a":1}{"b":2}` and the last name won. Now a fragment that carries a new call `id` opens the next call.

In the UI, case (1) shows real Writing/Saving cards before the stop, which matches the reported screenshot. Cases (2) and (3) show only "我正在执行下一步…" lines, with no tool card.

## Area

- [ ] Web UI / frontend
- [x] Agent / loop / delegation
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
- [ ] Test / harness
- [ ] Documentation
- [ ] Security-related change
- [ ] Release / packaging

## Verification

Ran:

```text
uv run pytest -q tests/test_llm_openai_tool_calls.py tests/test_agent_engine.py \
  tests/test_actions.py tests/test_agent_progress_circuit.py
uv run pytest -n auto --maxprocesses=4 --dist loadfile      # full offline suite, science extra: exit 0
uv run mypy                                                  # Success: no issues found in 25 source files
uv run python3 -m harness.cli run --tier pr --offline        # 38/38 passed
uv run pre-commit run --all-files                            # all hooks passed
uv run python scripts/check_directory_readmes.py             # complete bilingual coverage
python scripts/source_secret_scan.py                         # passed

Mutation check: reverting each fix turns its new tests red
  (engine note: 2 failed; empty arguments: 4 failed; missing index: 1 failed).

End to end: a scripted OpenAI-compatible relay drove a real daemon through real
Web turns over REST (streaming), plus `openai4s run` for the blocking path.
  0.3.0 and unpatched main: every scenario ends `failed` / `no_progress` after
    2-3 model calls.
  This branch: a model that follows the note sends the cell alone on the next
    call. The cell runs and `host.submit_output` completes the turn
    (`status: completed`). The empty-arguments call and both index-less
    parallel calls now execute.
```

Not run:

```text
browser E2E (node tests/browser_*.mjs); scripts/capture_response_schemas.py --check; a live LLM
```

Reason:

```text
No route, serializer or workbench change. The note only appends text to a
model-facing tool result, so response shapes are unchanged. I did not measure
which production relays send "" or drop `index`. The parser change accepts only
input that used to be an unconditional parse error.
```

## Risk and Reviewer Focus

- `openai4s/agent/engine.py`, `_note_unexecuted_cell`: the Engine decides routing, so this is the one boundary every executor passes through: Web, CLI, and delegated children. The note is appended to the last `role: "tool"` message's string content and to the observation string. It becomes part of the recorded tool result, so it also enters the progress circuit's result digest. The text is fixed, so a model that repeats itself still trips `same_action` at 3.
- `openai4s/llm/tooling.py`, `_parse_tool_arguments`: `""`, whitespace-only and `None` all become `("{}", {}, None)`. The string `"null"` and any other non-object JSON are still malformed. Stored history whose `raw_arguments` is `""` replays unchanged.
- `openai4s/llm/providers/openai.py`, `_fragment_index`: behavior changes only when `index` is absent or null. An explicit non-integer index keeps the old `len(calls)` fallback.

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
> Changes sit on the shared agent engine loop and LLM normalization path used by Web and CLI; behavior shifts only for mixed tool+cell replies, empty arguments, and missing stream indices.
>
> **Overview**
> Fixes three **input-side** paths that made the no-progress circuit end turns after two or three steps even when the model was behaving reasonably.
>
> When a reply mixes **native tool calls with a fenced code cell**, routing runs only the tools. The engine now appends a **system note** to the last tool result (and observation) explaining that the cell did not run and should be sent alone on the next turn. Models that ignore it still hit `same_action` as before.
>
> **OpenAI-compatible LLM parsing** now treats empty, whitespace-only, or null tool `arguments` as `{}` instead of a JSON parse error, and replays them as `"{}"`. **Streaming** tool-call assembly uses `_fragment_index` so relays that omit `tool_calls[].index` no longer merge parallel calls into one malformed batch.
>
> New tests cover the displaced-cell note, zero-argument calls, and index-less parallel streams.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit 96d1620ca6becc604cc35b98f310cd456173694c. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5d69f4b64a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.