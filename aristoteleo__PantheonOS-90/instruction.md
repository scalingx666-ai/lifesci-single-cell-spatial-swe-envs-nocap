# Issue

**Title:** Fix parallel call_agent display: tag streams with parent_tool_call_id

## Description

## Summary

When the main agent launches two parallel `call_agent()` invocations to the same agent name (e.g., two `researcher` sub-agents), the Timeline UI previously collapsed them into a single view — identical step counts, indistinguishable action lists. Two pieces of information were missing from the stream:
1. The child's `execution_context_id` never made it onto the `call_agent` tool response, so the frontend had no exec_id to scope by once the sub-agent finished.
2. While the sub-agents were still running (no tool response yet), streamed child messages had `execution_context_id` but no back-link to which parent `call_agent` tool_call they belonged to.

## Changes

- **`AgentRunContext.sub_agent_exec_ids`**: new dict mapping `parent tool_call_id → child execution_context_id`. `PantheonTeam.call_agent` records it right after building the child context; `Agent._call_tools` reads it when constructing the tool_message and stamps `execution_context_id` on the response so parallel siblings can be scoped post-completion.
- **`wrapped_step` / `wrapped_chunk`**: stamp `parent_tool_call_id` on every streamed child message. The UI can now pair `tool_call_id → execution_context_id` from the very first chunk, so parallel same-named sub-agents are distinguishable while still pending.

The UI side lives in pantheon-ui PR: https://github.com/Nanguage/pantheon-ui (branch `fix/sub-agent-card-parallel-dedup`).

## Test plan

- [x] `pytest tests/test_chat_rename_guards.py tests/test_conversation_recovery.py tests/test_responses_api.py tests/test_tool_result_vision.py` — 107 passed, 9 skipped
- [x] Smoke: `AgentRunContext(...).sub_agent_exec_ids` defaults to a fresh dict per instance
- [x] Manual: main agent launches two parallel `researcher` calls; while pending, each SubAgentCard shows its own step count and action list (previously identical)

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d277938d0cf4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.