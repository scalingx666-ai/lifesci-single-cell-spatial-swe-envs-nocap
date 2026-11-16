# Issue

**Title:** Fix chat auto-rename regressions + default OpenAI to Responses API

## Description

## Summary

Two separate fixes stacked on the same branch:

1. **Chat auto-rename**: fix three bugs where a "New Chat" either never got renamed on the first message, reverted back to "New Chat" on subsequent messages, or refused to ever rename again after being stuck in the revert loop.
2. **OpenAI routing**: default all non-codex OpenAI models to `/v1/responses`, falling back to `/v1/chat/completions` on per-endpoint 404. Unlocks native image input in tool results for `gpt-4o`, `gpt-5`, `gpt-5.4`, `o4-mini`, etc.

## Chat rename fixes (7e66573)

- **Msg-1 race**: rename task was scheduled *before* `thread.run()`, so it ran with empty memory and skipped. Moved it to after `thread.run()`.
- **Msg-2 revert**: `restoreSessionMetadata` was clobbering `memory.name` every turn with a stale `session_storage.metadata.customTitle` (set to "New Chat" on msg 1 and never synced when auto-rename succeeded). Once `name_generated=True`, `memory.name` is now authoritative and `customTitle` syncs the other way. `_background_rename_chat` also writes the new name into `customTitle` so the next turn reads the fresh value.
- **Stale-flag guard**: the hard "don't re-rename" guard keyed off `name_generated` was trapping chats that got stuck in the revert loop (`name_generated=True` + `name="New Chat"`). Switched the guard to key off the *actual name* — if `memory.name` is still a default placeholder, we retry regardless of the flag.
- **Tighter `_is_default_name`**: only matches known placeholders (`New Chat`, `New Chat in Project`, numbered variants, Chinese equivalents). Previously matched `startswith("Chat ")` which false-positived on AI names like "Chat about gene expression" and caused every turn to re-rename.

Tests: 10 new unit tests in `test_chat_rename_guards.py`, 1 regression test in `test_conversation_recovery.py` pinning the `customTitle` → `memory.name` precedence.

## OpenAI Responses API default (09680c8)

Motivation: the previous code only routed `codex/*` and `*-pro` through `/v1/responses`. Everything else — `gpt-4o`, `gpt-5`, `gpt-5.4`, `o4-mini` — went to Chat Completions, which rejects `image_url` in `tool` role messages. That forced `observe_images` into sub-agent text-summary mode even when the model itself had native vision, so users uploading an image saw a degraded pipeline.

Changes:
- `should_use_responses_api(config)`: new predicate. Returns True for all `ProviderType.OPENAI` except `codex/*` (has its own OAuth adapter) and `(base_url, model)` pairs marked unavailable in a per-process cache.
- `mark_responses_api_unavailable(config)` / `reset_responses_api_cache()`: cache control, populated on first 404.
- `call_llm_provider`: wrap `acompletion_responses` in `try/except openai.NotFoundError`. On 404, mark the cache and fall through to Chat Completions — unless `is_responses_api_model(config)` (Responses-only: `-pro`, codex-named), in which case the error propagates.
- `supports_tool_result_image`: keys off `should_use_responses_api` for OpenAI. Dropped the blanket "`LLM_API_BASE` set → return False" shortcut; proxies that *do* support Responses API no longer get misreported.

Non-OpenAI providers (`anthropic/`, `gemini/`, `ollama/`, `deepseek/`, `zai/`, `minimax/`, `moonshot/`, `qwen/`, `groq/`, `openrouter/`, `mistral/`, `together_ai/`, `gemini-cli/`) are untouched — all route through `ProviderType.NATIVE`.

Tests: `TestDefaultResponsesAPIRouting` covering cache-miss default, `(base_url, model)` cache isolation, 404 fallback, no-fallback for Responses-only models. Updated `test_tool_result_vision` for the new default, added cache-unavailable and native-provider-isolation cases.

## Test plan

- [x] `pytest tests/test_chat_rename_guards.py tests/test_conversation_recovery.py` — 18 passed
- [x] `pytest tests/test_responses_api.py tests/test_tool_result_vision.py` — 107 passed, 9 skipped (live-network tests)
- [x] Manual: send msg 1 → msg 2 → msg 3 in a fresh chat, confirm name sticks (regression reproduced pre-fix, gone post-fix)
- [x] Manual: upload image to `openai/gpt-5.4`, confirm the model sees it directly without invoking `observe_images`
- [ ] Manual: point `LLM_API_BASE` at a proxy that doesn't implement `/v1/responses`, confirm one 404 in logs followed by successful Chat Completions and no repeated probing

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4eec96a66c7f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.