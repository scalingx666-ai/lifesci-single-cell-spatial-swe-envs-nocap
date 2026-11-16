# Issue

**Title:** fix(chatroom): single-flight lock for per-chat team creation (port 3100 race / ve_curator tool loss)

## Description

## Problem
On Virtual Embryo sandboxes the curator intermittently either crashed at startup or reported its `ve_curator` KG tools as unavailable (`Tool 've_curator__kg_search' not found`).

Root cause: `ChatRoom.get_team_for_chat()` is **check-then-act with no concurrency guard**. Two near-simultaneous first-time requests for the same chat (e.g. the first user message racing a session restore) both miss the `chat_teams` cache and both run `_load_team_from_memory` → `_create_team_from_template`, each starting the team's endpoint + MCP gateway. The duplicate gateway races to bind `127.0.0.1:3100`:

- **hard failure**: `OSError: [Errno 98] address already in use` → `gateway.py` `SystemExit(1)` → sandbox `exit 1` → "no responders" → hub reaps the pod.
- **soft failure**: gateway comes up but `ve_curator` tools register on the losing instance, so the agent's active toolset lacks them → `ValueError: Tool 've_curator__kg_search' not found`.

(The default Pantheon app doesn't hit this — it has no MCP gateway competing for 3100, which is why only VE-app sessions broke.)

Sandbox log evidence: `_create_team_from_template 'Virtual Embryo Expert'` runs twice, `"Team ... created"` ×2, `"MCP server 've_curator' started successfully"` ×4.

## Fix
Wrap the cache-miss branch of `get_team_for_chat()` in a **per-chat `asyncio.Lock` with a double-check**, mirroring the existing `_ensure_project_endpoint` per-project lock. The team — and its endpoint/MCP gateway — is now built exactly once per chat; concurrent callers wait and reuse the cached team.

## Verified
- New concurrency check: 8 concurrent `get_team_for_chat` calls for the same chat → `_load_team_from_memory` runs **once**, all 8 get the same team; different chats still build independently.
- chatroom/team suite: **39 passed, 10 skipped**. (The 3 `test_chatroom_resilience::list_chats` failures are pre-existing on `main` — unrelated `project_manager` attribute, not touched here.)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee55298da535`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.