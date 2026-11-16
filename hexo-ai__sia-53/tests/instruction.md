# Issue

**Title:** feat: add OpenRouter provider and profiles

## Description

## Summary

Adds an `openrouter` provider and a matching meta/target profile pair, so a single
`OPENROUTER_API_KEY` can drive both the meta/feedback agent and the target agent across
400+ models without a per-vendor account.

There was previously no way to run SIA with only an OpenRouter key: no provider JSON
existed, and the bundled defaults (`default-meta` / `default-target`) require
`ANTHROPIC_API_KEY`.

Worth noting: #48 already added `_is_openrouter_provider()` to the pydantic-ai agent impl,
which matches on `provider.provider_id == "openrouter"` — but no such provider was bundled,
so that branch was unreachable. This PR supplies it.

## Type of change

Select all that apply:

- [ ] Bug fix
- [x] New feature
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

- `sia/defaults/providers/openrouter.json` — `client_kind: "openai"`, `base_url: "https://openrouter.ai/api/v1"`, `api_key_env: "OPENROUTER_API_KEY"`.
- `sia/defaults/profiles/openrouter-meta.json` — `agent_impl: "openhands"`, `model: "anthropic/claude-haiku-4.5"`. It uses `openhands` rather than `claude` because `_validate_meta` rejects `agent_impl: "claude"` paired with a non-anthropic provider (the Claude Agent SDK only talks to Anthropic).
- `sia/defaults/profiles/openrouter-target.json` — same model, `agent_reference: "default"`.
- `README.md` — `OPENROUTER_API_KEY` in the key-export list, plus a one-key quickstart.
- `docs/configuration.md` — bundled-provider list, two rows in the bundled-profiles table, the API-keys block, and a new *One OpenRouter key for both agents* section covering model-id namespacing.

No packaging change was needed: `[tool.setuptools.package-data]` already globs
`defaults/providers/*.json` and `defaults/profiles/*.json`. Verified all three JSONs land in a
built wheel, which matters for anyone using stock `sia` from PyPI without cloning.

## How I tested this

Full check suite, plus live calls against a real OpenRouter key on both agent paths.

```bash
python -m pytest tests/ -v          # 133 passed
ruff check sia/ tests/              # All checks passed!
ruff format --check sia/ tests/     # 51 files already formatted
ty check sia/                       # All checks passed!

# profiles resolve through the real loaders
python -c "from sia.profiles import load_meta_agent_profile as m, load_target_agent_profile as t; print(m('openrouter-meta')); print(t('openrouter-target'))"

# the new JSONs ship in the wheel
python -m build --wheel && unzip -l dist/*.whl | grep openrouter
```

Live verification against a funded OpenRouter key:

- **Target-agent client path** — `OpenAI(base_url=provider.base_url, api_key=os.environ[provider.api_key_env])` returned a completion served by `anthropic/claude-haiku-4.5`.
- **Meta-agent path** — `run_agent_openhands` with the `openrouter-meta` profile wrote a file, executed it, and exited 0. litellm routed correctly as `openai/anthropic/claude-haiku-4.5`.
- **Full `sia run`** — a `--max_gen 1` run on `spaceship-titanic` completed the orchestrator loop and generated a `target_agent.py` pointed at `https://openrouter.ai/api/v1` with `OPENROUTER_API_KEY`.

Two known issues found while testing are **not** addressed here and are being raised separately:

1. The generated target agent keeps the reference agent's Anthropic content-block response loop and crashes with `AttributeError: 'str' object has no attribute 'type'`. That is a gap in `build_target_client_setup` affecting every `client_kind: "openai"` provider, not just this one.
2. Prompt caching does not engage on this path (0.00% cache hit rate), which makes a gen-0 run cost ~$0.63.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bf7f77a47b3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.