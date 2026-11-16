# Issue

**Title:** fix: consolidate model profile UI and placeholder key handling

## Description

## Summary

This consolidates and supersedes #4 and #5 in one PR while preserving the original Grace-xyx authored commits in the branch history.

Kept from #4:
- Align configured model-profile rows with a scoped `.prof-row` grid.
- Move the activated model profile to the top of the configured profiles list.
- Document `webtools.py` next to the egress/security guidance.

Kept from #5:
- Treat obvious `.env.example` API-key stubs such as `your-api-key-here` as unconfigured.
- Prevent placeholder keys from showing as configured in model profiles.

Additional review fixes in this combined PR:
- Make placeholder filtering consistent across `LLMConfig`, `_llm_cfg`, runtime `llm_api_key` settings, profile create/edit/activate, profile masking, and built-in Ark profile seeding.
- Allow higher-priority placeholder env values to fall through to lower-priority real keys.
- Re-resolve API keys when switching providers so an old provider key is not carried into the new provider.
- Add regression coverage for placeholder fallthrough, `_llm_cfg`, profile masking, seed sanitization, and activation ordering.

## Contribution preservation

The two original commits from Grace-xyx are kept as authored commits in this branch:
- `fix(config): placeholder API key from .env.example falsely reported as configured`
- `feat(webui): align model-profile rows and move activated profile to top`

No squash was used, so the original author metadata remains visible for contribution attribution.

## Verification

- `uv run pre-commit run --all-files`
- `uv run pytest` → 191 passed, 2 skipped

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c7550f4a722`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.