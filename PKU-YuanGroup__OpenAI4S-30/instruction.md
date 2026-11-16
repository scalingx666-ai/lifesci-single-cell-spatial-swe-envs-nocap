# Issue

**Title:** Use protocol options for model profiles

## Description

## Summary

- replace the free-form model provider input with fixed OpenAI-compatible, Anthropic-compatible, and Ark-compatible protocol options
- enforce the same protocol allowlist in the model-profile service
- stop seeding built-in model endpoints and remove legacy generated presets with a one-time migration
- update the API contract and regression coverage

## Root cause

The Models settings UI used an editable input backed by the entire provider registry, so users could enter arbitrary provider values. The model-profile GET path also materialized every built-in model preset into saved profiles, which made a fresh configuration appear to contain many default endpoints.

## Impact

New installations start with an empty saved-endpoint list, users select one of three supported compatibility protocols, and existing customized profiles remain available. Legacy generated preset rows are cleaned up once.

## Validation

- `UV_CACHE_DIR=/tmp/openai4s-uv-cache uv run pytest -q`
- pre-commit hooks: end-of-file, line endings, whitespace, merge conflicts, isort, black, ruff, and strict mypy
- browser smoke test of the Models settings page, protocol selection, empty initial state, and profile creation

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a92e736b367e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.