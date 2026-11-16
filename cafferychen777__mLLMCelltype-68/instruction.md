# Issue

**Title:** feat(consensus): thread prompt_template through interactive_consensus_annotation

## Description

## Why

I ran into this building a multi-model consensus annotator on top of `interactive_consensus_annotation`. I wanted to reuse the consensus machinery for **cell-state** calls — different task framing and output contract (functional states, not cell-type labels), which means swapping the prompt.

Problem: there's no way to. `create_prompt` and `annotate_clusters` already take a `prompt_template`, but the consensus entry point neither accepts nor forwards one, so the initial phase is hard-wired to `DEFAULT_PROMPT_TEMPLATE`. The only workaround was monkeypatching the module global at runtime — fragile, and pinned to an exact version.

This just plumbs through the parameter that already exists one layer down.

## What

- `interactive_consensus_annotation` gains an optional `prompt_template` (default `None`), forwarded via `_run_initial_annotations` → `annotate_clusters`.
- Two behavioral tests: a custom template's text actually reaches the outgoing prompt; `None` still selects the default (provider stubbed, real `create_prompt` runs).
- CHANGELOG note under `[Unreleased]`.

When omitted, the prompt is byte-for-byte what it is today. Discussion prompts are untouched, and the cache key already derives from prompt text, so a new template gets its own cache entry.

## Tested

`pytest tests/` → 320 passed, 1 skipped (integration); `ruff check` clean. Checked the tests actually bite: drop the forwarding and the custom-template test fails (prompt falls back to default) while the default-template test stays green.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `200e4dc37c24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.