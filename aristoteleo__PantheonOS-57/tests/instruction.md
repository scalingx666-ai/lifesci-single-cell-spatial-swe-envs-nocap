# Issue

**Title:** fix: integrate token optimization with existing truncation layers

## Description

## Summary

Adapts PR#54's token optimization pipeline to work correctly with the existing two-layer tool output truncation system, fixing 8 identified issues and simplifying the architecture.

### Problem

PR#54's Stage 1 (Tool Result Budget) was completely ineffective because the existing Layer 2 (`process_tool_result` with `max_tool_content_length=10K`) already truncated all content before it reached the optimization pipeline. Two separate "save to disk + preview" mechanisms used different formats and couldn't recognize each other's output.

### Solution: Three-Layer Architecture

- **Layer 1 (tool-internal)**: Raised to 500K safety-valve role — prevents OOM from pathological output, no longer the primary truncation
- **Layer 2 (agent-level)**: Per-tool thresholds enforced at `process_tool_result()` time (grep 20K, read_file 40K, shell 50K), unified `<persisted-output>` format
- **Layer 3 (LLM view)**: Stage 1 simplified to aggregate-only safety net; Stages 2-5 handle history management

### Changes

- Unified externalization format (`<persisted-output>`) across `truncate.py` and `token_optimization.py`
- `process_tool_result()` accepts `tool_name`, uses `get_per_tool_limit()` for per-tool thresholds
- Removed `truncated`-field bypass of length limits (per-tool limits always apply; `truncated` flag only skips base64 filtering)
- `AgentRunContext` fields get default values for backward compatibility
- `_extract_read_paths_from_tool_calls` reads tool_call arguments instead of guessing from tool output content
- `build_llm_view_async` enables LLM-based autocompact in `_acompletion`
- `inject_cache_control_markers` adds litellm >= 1.34 version check
- Selective deepcopy for `cache_safe_prompt_messages`
- `build_llm_view` / `build_llm_view_async` share projection logic via `_prepare_llm_view_messages`
- `build_llm_view` filters non-standard message roles (defense against `for_llm=False` leakage)
- `max_tool_content_length` raised to 50K as per-tool fallback

## Test plan

- [x] 78/78 tests passing (58 original + 7 new adaptation + 13 truncate)
- [x] Per-tool thresholds verified at `process_tool_result` level
- [x] Unified format recognized by `_is_already_externalized` (Layer 2 ↔ Layer 3)
- [x] End-to-end: Layer 2 externalizes → Layer 3 preserves
- [x] `truncated` field no longer bypasses per-tool limits
- [x] Existing compression plugin unaffected (complementary design)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8f3c76084b38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.