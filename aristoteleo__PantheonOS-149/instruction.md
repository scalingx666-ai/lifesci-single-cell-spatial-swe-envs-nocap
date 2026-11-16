# Issue

**Title:** fix(mcp): bound MCP client connect/list/call with a timeout (fixes cold-start first-message hang)

## Description

## Problem
The FIRST chat message to a COLD sandbox hangs forever (the `chat` RPC never returns), while a WARM sandbox answers fine.

Root cause: `MCPProvider.list_tools()` (`pantheon/providers.py`) does `async with self._client: ...` with **no timeout**. It's awaited while assembling the tool list for the first LLM turn (`Agent.get_tools_for_llm`). On a cold sandbox the client's session establishment (connect to the unified MCP gateway, which proxies to the remote MCP server) can stall; `get_tools_for_llm`'s per-provider `try/except` catches *exceptions* but **not a hang**, so tool assembly blocks, the first completion is never issued, and the RPC never returns. `call_tool()` shares the same unguarded pattern.

Not app-specific — any agent with an MCP provider whose server is cold/slow (biomcp, context7, a remote HTTP MCP, …) can wedge the same way.

## Fix
Wrap both `async with self._client` blocks in `asyncio.wait_for` (bodies moved verbatim into nested coroutines, so the success path is behavior-identical).

- `list_tools` timeout → raises `TimeoutError`, which `get_tools_for_llm`'s existing `except` already catches → that provider is **skipped this turn** (the turn proceeds without its tools, retries once the MCP is warm) instead of hanging.
- `call_tool` timeout → raises, so the agent surfaces a tool error instead of blocking mid-turn.

Env-tunable: `PANTHEON_MCP_LIST_TIMEOUT_S` (default 30) / `PANTHEON_MCP_CALL_TIMEOUT_S` (default 120).

## Verified (locally)
- **Unit:** a fake MCP client whose session `__aenter__` hangs → `list_tools()` now raises `TimeoutError` in ~0.3s (was infinite); `get_tools_for_llm()` returns the healthy providers' tools and skips the hung one, in ~0.3s.
- **Regression:** `108 passed`. The 13 failures are pre-existing on `origin/main` (model-selector / provider-adapter catalog + `test_unified_mcp` E2E env) — confirmed identical via stash check.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c62653ec9439`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.