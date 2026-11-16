# Issue

**Title:** feat: rewrite Gemini adapter to use REST API instead of SDK

## Description

## Summary

- Rewrites the Gemini adapter from google-genai SDK to direct REST API calls (httpx), matching litellm's approach
- The SDK's internal serialization has known issues with tool call parameter mixing during parallel function calls
- The REST API handles tool calls reliably with proper JSON parsing

## Changes

- **`pantheon/utils/adapters/gemini_adapter.py`**: Complete rewrite
  - `httpx` streaming POST to `generativelanguage.googleapis.com`
  - SSE response parsing for streaming
  - v1alpha/v1beta version selection (gemini-3+ uses v1alpha)
  - UUID-based tool call IDs
  - REST API for embeddings
- **`tests/test_gemini_tool_calling.py`**: 3 integration tests validating tool call correctness

## Background

When using the google-genai SDK for tool calling, Gemini models sometimes mix parameters across parallel tool calls (e.g. `call_agent` receiving `file_path` and `content` from `write_file`). This did NOT happen when litellm called the same models via REST API. Root cause: the SDK's internal serialization/deserialization differs from the raw REST API.

## Test plan

- [x] 3 Gemini tool calling tests pass (simple, complex, many-tools)
- [x] Manual test with Gemini model in Pantheon UI — verified tool calls work correctly
- [x] Streaming text output works
- [ ] Verify thinking/reasoning output works

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba0d221dba31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.