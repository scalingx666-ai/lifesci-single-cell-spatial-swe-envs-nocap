# Issue

**Title:** fix(llm): rejoin interleaved indexless tool fragments by call ID

## Description

## Summary

### Introduction

The OpenAI Chat adapter already supports compatible relays that omit `tool_calls[].index`. When two calls arrive as `A(prefix), B(prefix), A(suffix), B(suffix)` and each fragment carries its call ID, the adapter currently opens a new accumulator whenever the ID differs from the latest call. Two well-formed calls become four incomplete calls with duplicate IDs and JSON parse errors, and the malformed declarations carry into assistant history.

Resolve an indexless fragment's existing wire ID before allocating a new accumulator. The change preserves first-declaration order and complete arguments. Explicit indices remain authoritative, and unidentified fragments retain the existing latest-call fallback.

The new regression fails on the unchanged upstream implementation for both fully indexless streams and indexed declarations followed by indexless continuations. After the fix, both cases retain two complete calls through normalization and next-turn history serialization. A separate check preserves explicit-index precedence.

This repairs the existing relay compatibility path; it does not claim that the strict OpenAI wire omits required indices. The governing contracts are the [wire adapter contract](https://github.com/PKU-YuanGroup/OpenAI4S/blob/ef85836a0b900799d7d478593080a84d64a86d8c/openai4s/llm/providers/README.md#adapter-contract) and the existing `test_streamed_parallel_calls_without_index_stay_separate` coverage. No external research claims are involved.

## Area

- [x] Agent / loop / delegation
- [x] Tests / harness / CI

## Change Type

- [x] Bug fix
- [x] Test / harness

## Verification

The same new tests against upstream before the source change:

```text
FF. [100%]
FAILED test_streamed_interleaved_calls_without_index_rejoin_by_id[False]
FAILED test_streamed_interleaved_calls_without_index_rejoin_by_id[True]
```

Focused verification after the fix:

```text
uv run pytest tests/test_llm_openai_tool_calls.py -k 'interleaved_calls_without_index or explicit_index_takes_precedence'
3 passed, 21 deselected

uv run pytest tests/test_llm_openai_tool_calls.py
24 passed
```

Full offline validation on macOS with the locked development environment:

```text
uv run pytest -n auto --maxprocesses=4 --dist loadfile -ra --durations=15
12134 passed, 150 skipped, 2 warnings in 743.52s

uv run mypy
Success: no issues found in 25 source files

uv run pre-commit run --all-files
All hooks passed

uv run python scripts/check_directory_readmes.py
199 maintained directories, complete bilingual coverage

uv run python scripts/source_secret_scan.py
Passed (exit 0)

git diff --check
Passed
```

The default suite retained its optional-dependency and platform skips. A separate loopback-only smoke also exercised the real HTTP/SSE transport and the next-turn serialized assistant history: two POSTs, two complete tool calls, zero external-provider or paid calls.

Not run: live provider calls or the full cross-platform release/browser matrix. This change is limited to the provider's existing fragment correlation helper; gateway routes, serializers, kernel protocols and UI code are untouched.

## Risk and Reviewer Focus

Review `_fragment_index` in `openai4s/llm/providers/openai.py` and the interleaved/replay regression in `tests/test_llm_openai_tool_calls.py`. The production change is four lines inside the existing indexless path plus its docstring. Matching uses an explicit wire ID, not tool name or argument content. Transport retries, stream completion/usage rules and tool execution permissions are unchanged.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot facades, workbench sources, vendored assets and captured fixtures were not changed.

### Tests

- [x] Relevant tests were run and listed above.
- [x] Default tests use only synthetic offline responses, without live LLM, network, GPU, SSH, Docker, lab hardware or secrets.
- [x] No tests were deleted.

### Core Dependency Policy

- [x] No hard third-party import was added to the core.
- [x] No optional science imports or dependency changes were introduced.

### Public Disclosure and Security

- [x] No secrets, credentials, private data or local absolute paths are included.
- [x] No unpublished research plans or experimental results are disclosed.
- [x] The change makes no new isolation, sandboxing or security guarantee.

### Docs

- [x] The function docstring matches the corrected behavior.
- [x] Translated README sections and public APIs are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef85836a0b90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.