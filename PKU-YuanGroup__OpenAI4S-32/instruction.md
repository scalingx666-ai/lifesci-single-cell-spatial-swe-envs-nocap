# Issue

**Title:** fix(web): stop offering endpoints the user never configured

## Description

## Problem

#30 stopped seeding the built-in model profiles into every user's saved list, but the header model selector kept exposing them from the other end.

`ModelProfileService.models_payload` built the dropdown from three sources: the live model, the saved profiles, **and every provider in the catalog**:

```python
for provider, spec in self._providers().items():
    add(spec.get("model"), spec.get("model"), provider)
```

So on a daemon configured only for `ark`, the selector still offered `gpt-5`, `claude-sonnet-4-5` and `gemini-2.5-flash`. There is no key for any of them, so picking one did nothing useful — it just failed at send time.

## Fix

The selector now lists the live model and the saved profiles, and nothing else.

A profile that leaves `model` blank still shows up, resolved through its protocol's default via `effective_model_id` — so "pick a protocol, don't name a model" keeps working. Previously such a profile only appeared because the catalog loop happened to add that same default.

The provider catalog itself is untouched: `_providers()` is still what `effective_model_id` resolves against. Only what the UI *offers* changed.

## Verification

Against a running daemon (`ark`, no profiles configured):

| | before | after |
|---|---|---|
| `GET /api/models` | `gpt-5`, `claude-sonnet-4-5`, `gemini-2.5-flash`, `doubao-seed-2.0-pro` | `doubao-seed-2.0-pro` |

Then adding a `claude` profile with a blank model brings `claude-sonnet-4-5` into the list, while `gpt-5` and `gemini-2.5-flash` stay out.

`test_header_selector_hides_endpoints_the_user_never_configured` pins both halves. The leak survived #30 because nothing asserted the selector's contents — the existing header test only checked the first entry and deduplication.

- `uv run pytest` — full offline suite passes
- `uv run pre-commit run` — clean

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5dd96588f5f8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.