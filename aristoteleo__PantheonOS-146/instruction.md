# Issue

**Title:** feat(llm): add Claude Sonnet 5 to the model catalog

## Description

## What

Adds **Claude Sonnet 5** (`claude-sonnet-5`) to the model catalog.

- **`pantheon/utils/llm_catalog.json`** — new `claude-sonnet-5` entry under the `anthropic` provider: 1M context, 128K max output, \$3/\$15 per 1M, vision / computer-use / reasoning / pdf all supported. `supports_assistant_prefill: false` to match the 4.6+ Anthropic API surface (assistant prefills 400), consistent with `claude-fable-5`.
- **`pantheon/utils/model_selector.py`** — prepend `anthropic/claude-sonnet-5` to the anthropic `normal` tier so it's reachable by tier routing (high/normal/low).

## Effect

- Surfaces in `list_available_models` → appears in the UI model picker automatically (the frontend fetches the list dynamically; **no frontend change needed**).
- Included in `reasoning_models` via `supports_reasoning`.

## Verification

`get_model_info` / `find_provider_for_model` / `completion_cost` / `list_available_models` all return the model correctly (cost \$18 @ 1M+1M = \$3+\$15). JSON validated; `model_selector.py` syntax-checked.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df6960cf8e01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.