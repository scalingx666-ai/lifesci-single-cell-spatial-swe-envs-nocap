# Issue

**Title:** feat: native image content in tool_result for capable providers

## Description

## Summary

Currently Pantheon always routes image observation through `observe_images`, a sub-agent that calls an internal VLM and returns a text summary. This was a conservative choice because OpenAI Chat Completions rejects image content in tool-role messages.

However, Anthropic Messages API, Gemini, OpenAI Responses API, and the Codex OAuth backend all support images in tool_result natively now. This PR adds a capability-detected fast path that embeds images directly in `tool_result`, so the main agent can see pictures across multiple turns (similar to Claude Code / OpenClaw).

## What changes

**Provider adapters (4):**
- `anthropic_adapter`: tool_result content carries native `{type:"image", source:{type:"base64",...}}` blocks.
- `gemini_adapter`: tool messages with images emit `functionResponse` + sibling `inline_data` parts.
- `openai_adapter`: sanitises images out of tool messages for Chat Completions (safety, avoids 400).
- `llm.py` (Responses API path): `function_call_output.output` is an array of `input_text` + `input_image` items when images are present. Shared by both the public Responses API (gpt-5.x-pro / codex-*) and the Codex OAuth backend.

**Tool framework (`agent.py`):**
- New `content_blocks` opt-in field on tool return dicts.
- When a tool returns `content_blocks` with images, the framework auto-merges JSON-serialized structured fields (cell_id, notebook_path, etc.) into a text block and prepends them to the blocks — no per-tool summary helper needed.
- Routes through `ImageStore` so base64 data URIs are persisted to disk as `file://` references (memory-efficient).

**Toolsets (2):**
- `observe_images`: native mode returns image blocks directly; sub-agent mode kept as fallback for Chat Completions.
- `integrated_notebook`: cell execution outputs include image blocks on native providers; `hidden_to_model` retained for Chat Completions safety.

**Helpers (2 new files):**
- `utils/vision_capability.py`: `supports_tool_result_image(model)` returns True for Anthropic / Gemini / Responses API / Codex OAuth. Returns False in proxy mode (`LLM_API_BASE` set) to avoid silent image stripping downstream.
- `utils/adapters/image_blocks.py`: shared `split_text_and_images`, `resolve_image_url`, `has_image_content`.

**Edge-case fixes found during testing:**
- `guard_empty_tool_results` previously replaced any non-string tool content with `[No output]` — silently dropped image payload lists. Fixed to treat `[text, image_url]` lists as non-empty.
- Codex OAuth (`codex/gpt-5.4`, `codex/gpt-5.2-codex`) was not recognised by capability detection, forcing sub-agent fallback. Added explicit `codex/*` support.
- Proxy mode (`LLM_API_BASE`) forces OpenAI Chat Completions regardless of model name — capability detection now returns False in proxy mode to preserve the sub-agent text summary.

**Prompt update (`visual_verification` partial):**
- New `prompts/visual_verification.md` (~900 tokens) instructing the agent to visually verify any generated plot/figure/screenshot via `observe_images` before presenting it. Covers when to verify vs skip, how to ask specific questions, findings → action mapping, and typical notebook patterns.
- Injected into Leader (`teams/default.md`) and Researcher (`agents/researcher.md`).

## Impact

| Provider | Before | After |
|---|---|---|
| Claude / Gemini / GPT Responses API / Codex OAuth | Sub-agent text summary only | Main agent sees the image, can multi-turn reason |
| GPT Chat Completions / Ollama / other OpenAI-compatible | Sub-agent fallback | **Unchanged** (sanitiser only activates if tool opts in) |
| Proxy mode (`LLM_API_BASE`) | Sub-agent text summary | **Unchanged** (capability detection returns False) |

## Test plan

**Unit tests (55, 0.4s):**
- [x] Capability detection (Anthropic / Gemini / Responses API / Codex / Chat Completions / proxy mode)
- [x] `image_blocks` helpers (data URI parsing, file:// resolution, edge cases)
- [x] Anthropic adapter (single / multiple images / HTTP URL)
- [x] Gemini adapter (inline_data parts, HTTP fallback)
- [x] OpenAI sanitiser (count placeholder, input immutability)
- [x] Responses API conversion helper
- [x] Agent-layer `content_blocks` detection
- [x] `observe_images` routing (native vs sub-agent)
- [x] `guard_empty_tool_results` preserves image lists, still replaces truly empty

**Integration tests — real APIs (7, 8.6s, `-m live_llm`):**
- [x] Anthropic reads marker from `tool_result` image block (claude-sonnet-4-5)
- [x] Gemini reads marker from `functionResponse + inline_data` (gemini-2.5-flash)
- [x] OpenAI Chat Completions does NOT 400 after sanitiser (gpt-5.4-mini, gpt-4o-mini)
- [x] OpenAI Responses API reads marker from `function_call_output` (gpt-5.2-codex)
- [x] Full `observe_images` native path end-to-end via Anthropic
- [x] Native mode preserves structured metadata (Claude reads BOTH `cell_id` AND image marker)

**Manual testing:**
- [x] `codex/gpt-5.4` via real chat: DNA icon correctly identified (uncovered two fixes above)
- [x] Anthropic and Gemini providers tested via live chat

Run:
```
pytest tests/test_tool_result_vision.py                            # unit
pytest tests/test_tool_result_vision_integration.py -m live_llm    # with API keys
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8342f2f07484`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.