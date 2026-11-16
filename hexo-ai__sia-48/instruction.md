# Issue

**Title:** fix: harden OpenRouter target runs

## Description

Summary:
- resolve OpenRouter PydanticAI profiles through the native OpenRouter provider and require the configured API key
- wrap malformed 200/JSON provider responses with actionable context
- require generated target agents to bound API timeouts/retries and update the GPQA reference agent

Tests:
- python -m pytest tests/ -v
- ruff check sia/ tests/
- ruff format --check sia/ tests/
- ty check sia/ (passes with existing optional google.generativeai unresolved-import warning)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c503030815f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.