# Issue

**Title:** Fix Gemini image-gen output and reload_settings RPC

## Description

## Summary

Two bugs on the image-generation path:

1. `generate_image` calls targeting Gemini image models returned `{"success": true, "images": []}` — the bytes were arriving but got dropped by the adapter.
2. The "Reload Settings" button in the right-sidebar Config tab did nothing — the RPC method existed but was never registered as a tool.

## Gemini image output (b6f202f)

- **`gemini_adapter.acompletion`**: the SSE part parser handled `text`, `functionCall`, and `thought` parts but had **no branch for `inlineData`**. Gemini emits image bytes under that key, so the payload was silently skipped. Added a branch that wraps each inline payload as `data:<mime>;base64,<data>` and appends an `images` delta chunk. Also logs a warning on non-normal candidate `finishReason` values (`SAFETY` / `RECITATION` / `IMAGE_SAFETY` / `OTHER`) so future policy blocks are visible in the log.
- **`stream_chunk_builder`**: didn't aggregate `images` deltas into the assembled message, so even if the adapter emitted them, downstream `ImageGenerationToolSet._multimodal_image_gen` would see `message.images == None`. Added `full_images` accumulation and exposed it on the synthesised message (+ `model_dump`).

Reproduced against `gemini-3.1-flash-image-preview` (Nano Banana 2); after the fix the tool returns a list of saved image paths and the UI renders them.

## Reload settings (2fdb5b3)

`ChatRoom.reload_settings` was defined but missing the `@tool` decorator, so `service.invoke('reload_settings')` had no registered handler. Users had to restart the backend for edits to `.env` or `settings.json` (e.g. switching `image_gen_model` between providers) to take effect, even though the underlying `Settings.reload()` path exists. Added the decorator.

## Tests

- New `tests/test_gemini_image_output.py`:
  - `stream_chunk_builder` aggregation
  - no-image fall-through (`message.images` stays `None`, not `[]`)
  - end-to-end fake-httpx SSE run through `GeminiAdapter.acompletion`
- `pytest tests/test_gemini_image_output.py tests/test_gemini_adapter_base_url.py tests/test_gemini_tool_calling.py tests/test_tool_result_vision.py tests/test_chat_rename_guards.py tests/test_conversation_recovery.py` — 80 passed

## Test plan

- [x] Unit tests: 80 passed
- [x] Manual: call `generate_image` with Gemini `gemini-3.1-flash-image-preview` — image saved to disk and rendered in chat
- [x] Manual: edit `settings.json`, click "Reload Settings" in the right sidebar — new `image_gen_model` picked up without restarting the backend

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31081ef365c0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.