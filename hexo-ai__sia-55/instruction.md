# Issue

**Title:** fix: route gateways via their own litellm provider so prompt caching works

## Description

> Builds on #53 (now merged); rebased onto `main`.

## Summary

Prompt caching was silently dead on **every** OpenAI-compatible gateway, and the meta agent's
context window and cost were undetectable. A gen-0 run on OpenRouter cost **$0.63** with a
**0.00% cache hit rate** on every turn — 400K cumulative input tokens re-sent across 20 turns.

Two independent causes:

1. **litellm strips the breakpoints.** `_resolve_model` hardcoded an `openai/` prefix, so litellm resolved `custom_llm_provider="openai"` and `OpenAIGPTConfig.remove_cache_control_flag_from_messages_and_tools` (`litellm/llms/openai/chat/gpt_transformation.py:400-420`, called unconditionally at `:438`) recursively deleted every `cache_control` key before the request was serialised. OpenHands emitted them correctly; litellm dropped them with no error and no warning.
2. **The capability gate never fired.** OpenHands keys `PROMPT_CACHE_MODELS` on the vendor's hyphenated id (`claude-haiku-4-5`), but a gateway routes by its own id (`anthropic/claude-haiku-4.5`). The substring match failed, and litellm could not map the model at all — leaving `max_input_tokens` and `max_output_tokens` as `None` and cost reported as `$0.00`.

Both become configuration rather than code, so a new gateway or model needs no code change.

| | before | after |
|---|---|---|
| `cache_control` on the wire | stripped | present |
| `max_input_tokens` | `None` | 200000 |
| `max_output_tokens` | `None` | 64000 |
| cost per turn | `$0.00` | real |

## Type of change

Select all that apply:

- [x] Bug fix
- [ ] New feature
- [x] Documentation
- [ ] New or updated task
- [ ] Evaluation change
- [x] Provider/model configuration
- [ ] Security-sensitive change
- [ ] Refactor / maintenance
- [ ] Other

## Related issue

Closes #

## What changed

- **`sia/providers.py`** — `Provider` gains optional `litellm_prefix` (default `"openai"`). Providers that omit it behave byte-identically to before.
- **`sia/defaults/providers/openrouter.json`** — sets `"litellm_prefix": "openrouter"`, so litellm applies `OpenrouterConfig`, which preserves `cache_control` (`transformation.py:91-102`), hoists tool-message markers into content blocks as OpenRouter requires (`:103-145`), and adds `usage: {include: true}` (`:167-169`).
- **`sia/profiles.py`** — `MetaAgentProfile` gains optional `model_canonical_name`, used **only** for SDK capability lookups while `model` stays the routing id.
- **`sia/defaults/profiles/openrouter-meta.json`** — sets `"model_canonical_name": "claude-haiku-4-5"`.
- **`sia/agent_impls/openhands.py`** — `_resolve_model` uses the provider-declared prefix; the canonical name is passed to `LLM(...)`; **`reasoning_effort` is pinned to `None`** (see below); a warning fires if the installed SDK ignored the canonical name.
- **`sia/agent_impls/base.py`, `sia/orchestrator.py`** — thread the canonical name from the profile to the impl.
- **`docs/configuration.md`** — documents both fields and corrects the OpenRouter section.

### Why `reasoning_effort=None`

Naming a gateway's litellm provider has a side effect that has nothing to do with caching: the SDK
defaults `reasoning_effort` to `"high"` (`llm.py:358-364`) and only sends it when litellm reports
the provider reasoning-capable — true for `openrouter/…`, false for `openai/…`. Captured bodies,
same messages, only the prefix differing:

```
openai/…      {'model': 'anthropic/claude-haiku-4.5'}
openrouter/…  {'model': ..., 'max_completion_tokens': 64000,
               'reasoning_effort': 'high', 'usage': {'include': True}}
```

That is extended thinking at high budget — more output tokens, higher latency, different tool
behaviour. Shipping it inside a caching fix would make any measured cost delta uninterpretable, so
it is pinned off. Enabling thinking should be a separate change with its own before/after eval.

### Backward compatibility

The canonical name is forwarded **only when set**, so runners registered against the older
signature keep working — `register()` is a documented extension point (`base.py:5-9`) and
`AgentRunner` is `Callable[..., Awaitable[None]]`, so no type checker would catch a break. When the
value *is* set and a runner cannot accept it, the `TypeError` is loud rather than a silently
ignored capability.

## How I tested this

```bash
python -m pytest tests/ -v          # 139 passed (133 before, 6 new)
ruff check sia/ tests/              # All checks passed!
ruff format --check sia/ tests/     # 51 files already formatted
ty check sia/                       # All checks passed!
```

New tests:

- `test_openrouter_prefix_preserves_cache_control_on_the_wire` — monkeypatches the HTTP transport and asserts `cache_control` is present in the **serialised request body** under `openrouter/` and absent under `openai/`, that `reasoning_effort` is not sent, and that the token limits are populated. Asserting on the capability flag alone would prove nothing: it reports caching active in *both* cases — only the payload differs. No network, no spend.
- `test_openhands_model_uses_provider_declared_litellm_prefix` — covers the new prefix, no double-prefixing, that `nebius` is unchanged, and that `openai/gpt-oss-120b` on a gateway is now correctly prefixed (the old hardcoded `startswith("openai/")` guard skipped it and left it misrouted — a latent bug this fixes).
- `test_run_agent_forwards_model_canonical_name_only_when_set` — covers both branches of the conditional forwarding, including a legacy runner signature.
- Optional-field loading tests for both `litellm_prefix` and `model_canonical_name`.

The wire-capture test uses `pytest.importorskip("openhands")`, matching the existing `pydantic_ai`
test, so **it skips in CI** where optional SDKs are not installed. It runs for anyone following the
CONTRIBUTING dev setup.

**Not yet measured live.** The predicted saving is inferred from the payload and the published
cache multipliers (writes 1.25×, reads 0.1×), not observed on a real run — the test key's credit
cap could not fund a second gen-0. Someone should confirm a non-zero cache hit rate and the actual
dollar delta before we quote a number.

## Known limitation, deliberately out of scope

`sia/context_manager.py:155-161` calls `run_agent` **without a provider**, so the per-generation
summariser resolves `anthropic/claude-haiku-4.5` with no base_url and `sia/api_keys.py:21` reaches
for `ANTHROPIC_API_KEY`. An OpenRouter-only user gets a 401 against `api.anthropic.com`, and the
failure is swallowed (`context_manager.py:167-172` returns `None`), so generation summaries go
silently missing. That predates this PR and needs `ContextManager` to receive the profile; flagging
it here so the summariser still being empty is not mistaken for this fix not working.

## Security and privacy checklist

- [x] This change does not log API keys, secrets, private task data, or generated credentials.
- [x] This change does not weaken sandboxing, subprocess isolation, or task data boundaries.
- [ ] Security-sensitive behavior is explained in the PR description.
- [x] Not applicable.

## Documentation checklist

- [x] I updated README.md, CONTRIBUTING.md, SECURITY.md, or docs files as needed.
- [x] I added or updated examples where helpful.
- [ ] Documentation is not needed for this change.

## Contributor checklist

- [x] I ran the relevant tests.
- [x] I ran linting and formatting checks.
- [x] I kept the PR focused on one logical change.
- [x] I reviewed my own diff before requesting review.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01HPkffXZbzVPFLiaEy2PRfB

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `233fdea670d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.