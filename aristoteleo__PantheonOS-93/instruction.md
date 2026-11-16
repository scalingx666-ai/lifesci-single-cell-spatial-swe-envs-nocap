# Issue

**Title:** OAuth: frontend-driven browser flow + Gemini CLI adapter fixes

## Description

## Summary

Two related groups of changes that land together.

### 1. OAuth login flow (`69c76ca`)

Splits the backend's all-in-one `login()` into `start_login` / `wait_login` / `complete_login_from_url` / `cancel_login`, so the frontend can drive `window.open(auth_url)` on the user's own browser instead of relying on the backend Python process to spawn a tab. Adds a manual paste-URL fallback for setups where the backend's callback host is unreachable from the user's browser (remote / WSL1 / docker without port mapping). Fixes:

- WSL: Python side often can't spawn the Windows default browser reliably.
- Remote/headless: `webbrowser.open` has nothing to open.
- Homebrew Gemini CLI installs: `extract_gemini_cli_credentials` now handles the bundled `bundle/chunk-*.js` layout (not just npm-style `oauth2.js`) and prefers the anchored `OAUTH_CLIENT_ID = "..."` assignment over the loose regex so it doesn't pick `CLOUD_SDK_CLIENT_ID` by mistake.
- The `@tool` decorator's `session_id → client_id` back-compat alias was stealing the argument from tools that declare `session_id` themselves; now guarded by `"session_id" not in params`.

New tools in `ChatRoom`: `oauth_start`, `oauth_wait`, `oauth_complete`, `oauth_cancel`. Legacy `oauth_login` kept for back-compat.

Frontend companion PR: https://github.com/Nanguage/pantheon-ui (`feat/oauth-paste-and-tool-details`).

### 2. Gemini CLI adapter parallel tool-call fixes (`f22e1d7`)

`gemini-cli/gemini-3.1-pro` likes to emit multiple `functionCall` parts per turn. Two bugs broke that:

- `_extract_gemini_text_and_tool_calls` appended tool_call dicts without an `index` field → `stream_chunk_builder` defaults missing index to 0 → all calls got `+=` into one `function.arguments` → invalid JSON like `{a:1}{b:2}` → "Failed to parse tool arguments: Extra data" on every retry.
- `_messages_to_gemini_rest_contents` emitted each OpenAI-style tool response as its own `user` content. Gemini requires *N* `functionResponse` parts in the user turn to match *N* `functionCall` parts in the preceding model turn, so two parallel tool responses → 2 separate user contents with 1 part each → HTTP 400 "Please ensure that the number of function response parts is equal to the number of function call parts of the function call turn."

Fixed both: add per-extractor `tool_call_idx += 1`, and coalesce consecutive `role:"tool"` messages into a single `user` content with N `functionResponse` parts.

## Test plan

- [x] `pytest tests/test_oauth_split_flow.py` — 11 passed
- [x] `pytest tests/test_gemini_cli_adapter_parsing.py` — 7 passed
- [x] `pytest tests/test_gemini_oauth.py` — 9 passed (no regressions on old OAuth suite)
- [x] Manual: click Codex Login in the UI → tab opens on user's browser → auto-complete via callback server
- [x] Manual: click Gemini Login → OAuth completes, token exchange uses correct `OAUTH_CLIENT_ID`
- [x] Manual: `gemini-cli/gemini-3.1-pro` with parallel `write_file` calls — arguments parse cleanly, no 400

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b7aad6bd460b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.