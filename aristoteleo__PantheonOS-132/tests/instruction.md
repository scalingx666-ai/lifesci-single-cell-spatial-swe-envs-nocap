# Issue

**Title:** feat: platform-budget force-proxy + budget-aware quality tiers

## Description

Backend for the local/desktop platform-budget feature. All opt-in + inert unless a client turns it on via the `set_llm_proxy` RPC.

- `acompletion` force-proxy mode (utils/llm.py): when LLM_FORCE_PROXY is set, route non-OAuth providers through the platform proxy (PANTHEON_PLATFORM_PROXY_BASE/KEY), keeping adapter/model selection.
- `set_llm_proxy(enabled, base_url, api_key)` RPC (chatroom/room.py) — frontend-only; resets the model selector on toggle.
- Budget-aware quality tiers (utils/model_selector.py): under force-proxy, high/normal/low resolve only to platform providers (anthropic/openai/gemini), never a local-only one.
- `[PLATFORM-BUDGET-ROUTE]` log when a call routes through the proxy.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15aacd5fcf7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.