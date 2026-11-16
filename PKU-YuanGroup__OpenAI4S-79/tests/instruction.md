# Issue

**Title:** Add Anthropic Messages SSE streaming

## Description

## Summary

Add real Server-Sent Events streaming to the Anthropic Messages adapter.

- Send `stream: true` when an `on_delta` callback is present.
- Forward text deltas as they arrive and reconstruct the final normalized reply.
- Reassemble streamed tool-use JSON fragments and merge usage metadata.
- Preserve the existing blocking path when streaming is disabled or cannot start.
- Mark the built-in Claude provider as streaming-capable and wire both transports to it.

## Area

- [x] Tests / harness / CI

LLM provider adapter and capability routing.

## Change Type

- [x] Bug fix

## Verification

Ran:

```text
python3 -m pytest --noconftest -q tests/test_llm_anthropic_streaming.py tests/test_llm_providers.py tests/test_llm_capabilities.py tests/test_llm_transport_wiring.py
# 46 passed

python3 -m black --check openai4s/llm/providers/anthropic.py openai4s/llm/client.py openai4s/llm/capabilities.py tests/test_llm_anthropic_streaming.py
# 4 files would be left unchanged
```

Not run:

```text
uv run pytest
uv run pre-commit run --all-files
```

Reason:

```text
The local checkout is a blob-filtered sparse clone after repeated GitHub pack
transfer failures. Focused offline regression tests and formatting checks pass;
the full repository gates are left to CI.
```

## Risk and Reviewer Focus

Please review the Anthropic event-to-content reconstruction, especially the
boundary between safe blocking fallback (no event received) and stream errors
after delivery has started. The tests cover text deltas, usage merging,
tool-input JSON fragments, non-replay after a started stream, and blocking
fallback before the first event.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.
- [x] Hotspot files were edited surgically if touched: `gateway.py`,
      `host_dispatch.py`, `store.py`, `app.js`, `worker.py`, `manager.py`.
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
- [x] `README.md` and `README_zh.md` stay in sync where translated sections are
      affected.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9be2fe687d9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.