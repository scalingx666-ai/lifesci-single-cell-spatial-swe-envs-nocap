# Issue

**Title:** fix(desktop): carry the platform's model mode into the local backend

## Description

Desktop users with platform budget saw only the 3 native proxy families in the model picker, while a hub-served client gets the full OpenRouter catalog. The local backend never sees the deployment's `PLATFORM_MODEL_MODE` env, so `list_models` had no platform view to offer and `openrouter/<vendor>/<model>` picks failed provider validation.

`set_llm_proxy` now accepts `model_mode`: the frontend forwards the deployment's mode with the proxy creds (Nanguage/pantheon-ui#36), and the RPC mirrors it into this process — set on `openrouter`, cleared on `direct`/disable, untouched when an older frontend omits it. Regression tests cover all four transitions.

. Shipped in desktop 0.3.8.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01SS9mntiDnmsJ7tV8qYFGWc

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ca59439d1298`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.