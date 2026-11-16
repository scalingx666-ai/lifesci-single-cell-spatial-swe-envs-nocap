# Issue

**Title:** fix: guard context budgets before fallback routing

## Description

## Problem
Fallback routing could forward a model's advertised output budget without accounting for the current prompt, tools, or the smaller fallback model's context window. Automatic compression also ignored the pending user turn and could miss a changed active tool schema.

## Change
- Clamp chat, Responses API, and OpenAI-compatible fallback output-token parameters to the model's remaining context budget, with a safety margin, and fail before a provider call when no output can fit.
- Normalize structured pending input and include pending messages, output reserve, and tool-schema deltas in compression preflight.
- Persist the tool-definition token estimate with assistant metadata and count tool-call/function-call payloads in both normal and fallback token estimation.
- Keep context exhaustion on the normal model chain: skip the exhausted candidate and try the next model without issuing a provider request for the failed candidate.

## Validation
- `uv run --no-sync pytest -q tests/test_context_budget.py tests/test_compression.py tests/test_responses_api.py -k 'not live'` — 102 passed, 12 skipped.
- Mocked chat/fallback and Responses API calls assert the clamped parameter reaches the adapter/client; a model-chain test covers context-only fallback.
- `python3 -m compileall -q pantheon tests/test_context_budget.py` and `git diff --check` passed.
- No real LLM requests were made. The repository-wide CI job still includes unrelated live-provider and pre-existing tests; those failures are documented in the run logs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d3d459ac575`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.