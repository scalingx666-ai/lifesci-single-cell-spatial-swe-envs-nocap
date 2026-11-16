# Issue

**Title:** feat(retrosynthesis): add evidence-backed route triage

## Description

## Summary

This PR evolves the retrosynthesis planning skill from route visualization into an evidence-backed route-triage workflow.

- Adds optional RDKit support to the `science` environment so route dashboards use self-contained, transparent-background molecular depictions.
- Adds source-backed Step Evidence cards to route views and the interactive reaction graph.
- Adds `OpenAI4SLLMReactionEvidenceProvider`, which explicitly orchestrates `host.llm` with `host.web_search` and optional `host.web_fetch`: the model plans chemistry-aware queries, retrieval returns the sources, and the model may select only returned source IDs.
- Supports optional DOI resolution through the active `literature-review` skill. A resolving DOI verifies the identifier only; it never upgrades a candidate into verified reaction precedent.
- Adds auditable execution scoring and project constraints across backend score, step efficiency, terminal-stock coverage, evidence coverage, and constraint fit.

## Safety and Evidence Policy

LLM-generated URLs, titles, yields, conditions, and verification claims are never accepted as source evidence. Retrieved records remain clearly labeled as candidate sources requiring chemist review, receive capped evidence coverage, and cannot silently become verified exact-substrate precedent. Live LLM/network calls are opt-in through the provider; offline route ranking retains its legacy behavior when no evidence, constraints, or custom weights are supplied.

## Documentation

`skills/retrosynthesis_planning/SKILL.md` now documents the OpenAI4S retrieval composition and the review/promotion boundary for candidate evidence.

## Verification

```text
uv run python -m pytest -p no:capture tests/test_retrosynthesis_planning.py -q
uv run pre-commit run --files skills/retrosynthesis_planning/SKILL.md skills/retrosynthesis_planning/kernel.py tests/test_retrosynthesis_planning.py
git diff --check
```

All 29 focused tests passed. Pre-commit checks passed: isort, black, ruff, and mypy.

## Reviewer Focus

- `skills/retrosynthesis_planning/kernel.py`: source-ID grounding, candidate-vs-verified handling, and the legacy-safe ranking path.
- `tests/test_retrosynthesis_planning.py`: mocked LLM/search flow proves invented source IDs are discarded and candidate evidence remains capped.
- `skills/retrosynthesis_planning/SKILL.md`: the runtime wiring requires `host.llm`, `host.web_search`, optional `host.web_fetch`, and optionally `verify_dois` from the active literature-review skill.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `78dada64fa7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.