# Issue

**Title:** fix(agent): keep MCP tools foreground-only (fixes ve_curator 'tool not found' in background_task)

## Description

## Problem
On VE sandboxes, after the team-init race fix (#134) the curator correctly saw `ve_curator__*` tools but every KG call still failed with:
`Tool 've_curator__kg_search' not found. Available tools: ['background_task','think','file_manager__*',...]` — note **no `ve_curator__*` in the list**, but `file_manager__*` (local toolset) **was** present.

**Root cause:** the LLM set `_background: true` on the MCP tool calls, so they ran inside `background_task()` — a **separate `asyncio.Task`** (`background.py: asyncio.create_task`). MCP provider sessions are **task-bound** (the MCP client lives on the endpoint's main task). Cross-task access makes `provider.list_tools()` raise, which `call_tool` swallows in its `except` (`agent.py:1211`), so MCP tools drop out of the resolved tool table → "not found". Local toolsets aren't task-bound, so they stayed visible — exactly matching the symptom.

`get_tools_for_llm` injects a `_background` param into **every** eligible tool schema (`agent.py:1037`), so the LLM was free to choose background execution for MCP tools too.

## Fix
`get_tools_for_llm()` now detects `MCPProvider` instances and **omits `_background` from their tool schemas**. The LLM can no longer request background execution for MCP tools, so they run foreground on the main task where the session is valid. Mirrors the existing `_BG_PARAM_SKIP` (`background_task`/`think`/`call_agent`). Local + base tools keep `_background`.

Schema-layer change (not execution-layer) — there's no risk of the agent believing a tool is backgrounded when it isn't.

## Verified (locally)
- **Unit:** MCP provider tools (`ve_curator__*`) have **no** `_background`; local provider tools (`file_manager__*`) and normal base tools (`list_agents`) **keep** it; `_BG_PARAM_SKIP` tools (`think`) unchanged.
- **Regression:** `152 passed, 65 skipped`. The failures are pre-existing on `main` (model-selector / provider-adapter config + a `test_unified_mcp` E2E env RecursionError) — confirmed identical on a clean `origin/main` via stash check.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1a0ce41d8496`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.