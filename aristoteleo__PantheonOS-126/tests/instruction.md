# Issue

**Title:** fix(adapters): bound LLM request timeout so a stalled endpoint fails fast

## Description

## Problem

`AnthropicAdapter` and `OpenAIAdapter` construct their SDK clients with no timeout, so a stalled/hung endpoint blocks on the SDK default (~600s). In headless/benchmark runs this looked like a freeze for many minutes — in one case a container stayed wedged for ~1h before being killed.

## Fix

When building each client, pass:
```python
kwargs = {"timeout": httpx.Timeout(120.0, connect=10.0), "max_retries": 0}
```
- a stall now fails fast at ~120s (10s connect);
- `max_retries=0` so the SDK doesn't *also* retry — pantheon's own `num_retries` loop owns retries.

## Scope
Touches only client construction in the two adapters. **Independent of and complementary to `4307a4c`** (skip-empty-messages) — that fix is preserved untouched.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b97778d991bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.