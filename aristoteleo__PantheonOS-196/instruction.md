# Issue

**Title:** Desktop model access

## Description

## Summary
- Replaces the runtime half of #193 with a linear, single-commit history based directly on current `main` (no docs changes, no upstream merge commits).
- Restores Desktop multi-provider model access under platform budget (`_effective_providers()`), treats `PANTHEON_PLATFORM_PROXY_*` as force-proxy so credits are used, and accepts OpenRouter-prefixed platform model ids in provider validation.
- Includes the matching create/update regression tests in the same commit so the picker/proxy changes are not mergeable without the OpenRouter validation fix.

This is the same runtime change as #193 (`room.py`, `llm_providers.py`, `model_selector.py`, `tests/test_chatroom_platform_model_validation.py`). Please review and merge this PR independently; #193 is left open as the review reference.

## Test plan
- [ ] `pytest tests/test_chatroom_platform_model_validation.py`
- [ ] Desktop picker lists Anthropic/Gemini/OpenAI when platform proxy env is set
- [ ] Selecting `openrouter/<vendor>/<model>` passes create/update validation
- [ ] History is one commit on current `main` and can merge without squash

Made with [Cursor](https://cursor.com)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7bb8bd3a83e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.