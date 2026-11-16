# Issue

**Title:** fix(file_manager): output-token truncation guards + append_file tool (clean cherry-pick from #55)

## Description

## Summary

Clean cherry-pick of the feature commits from PR #55, **without** the problematic revert history in the `dev` branch.

### Problem with PR #55

PR #55 (`dev` → `main`) carried revert history from `dev` that would **erroneously delete** files restored by PR #63:
- `pantheon/utils/token_optimization.py` (-1,776 lines)
- `tests/test_token_optimization.py` (-1,498 lines)
- `scripts/benchmark_prompt_cache.py` (-385 lines)
- `scripts/benchmark_token_optimizations.py` (-535 lines)
- Plus rollback of token optimization integration in `agent.py`, `pantheon.py`, `truncate.py`

This happened because `dev` merged main's revert commit (`3f1343a`) via PR #61, so its diff against current main shows deletions of files that PR #63 just restored.

### Solution

Cherry-picked only the 4 actual feature commits from `dev`, skipping all merge/revert commits:

1. `c6e57e4` — fix(prompts): add failure recovery protocol and scientific writing gate
2. `e3e073f` — fix(file_manager): add output-token truncation guards and append_file tool
3. `c37a3c7` — test: add comprehensive tests for output-token truncation guards
4. `7920a72` — fix(llm): set max_tokens to model's max output + raise tool guard thresholds

### Changes

- `pantheon/toolsets/file/file_manager.py` — output-token truncation guards, append_file tool, size formatting
- `pantheon/utils/llm.py` — set max_tokens from model's max_output_tokens
- `pantheon/factory/templates/prompts/delegation.md` — failure recovery protocol
- `pantheon/factory/templates/teams/default.md` — scientific writing gate
- `tests/test_file_manager.py` — comprehensive truncation guard tests

### What's NOT included (intentionally)

All token optimization deletions from the `dev` branch revert history — those files are preserved intact from PR #63.

## Test plan

- [ ] `pytest tests/test_file_manager.py` — new truncation guard tests pass
- [x] Verify no token optimization files are affected
- [x] PR #55 can be closed after this merges

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0335885b4fc0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.