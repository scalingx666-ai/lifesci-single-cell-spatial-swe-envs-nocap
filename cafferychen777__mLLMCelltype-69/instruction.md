# Issue

**Title:** feat(providers): optional token-usage capture via usage_sink

## Description

## Context

Follow-up from #68 — thanks again for merging that one (and for the positional-compat shim).

This one is less clear-cut, so I'm opening it as a **proposal**, it touches the `list[str]` return contract that every provider shares,
and you'll see call sites, packaging, and CI implications on your side that I can't from a local checkout.
Happy to reshape or narrow it to whatever fits your vision for the provider layer — or to drop it if you'd rather solve usage tracking a different way.

## The problem I'm trying to solve

Downstream I need per-call token usage (and OpenRouter's native USD cost) to cost-account a consensus run. Currently the library seems to discard it: every `process_*` returns `list[str]`, the OpenAI-compatible parser keeps only `choices[0].message.content`, and Gemini reads only `response.text`. So I currently recover usage by monkeypatching `requests.post` and `google.genai`'s `generate_content` around `interactive_consensus_annotation` — fragile and pinned to an exact version. I'd love a small supported seam so that patch can go away, and figured others doing cost accounting hit the same wall.

## One way to do it (this PR)

An **opt-in** `usage_sink: dict | None = None`:

- On the OpenAI-compatible providers and Gemini, and on the shared `call_openai_compatible_api` / `call_http_api_with_retry` core. When passed, it's filled **in place** with `{prompt_tokens, completion_tokens, total_tokens}` — plus `cost` (USD) for OpenRouter, which opts into `usage: {include: true}` *only* when a sink is supplied.
- Gemini's `usage_metadata` normalizes to that same schema.
- Two public extractors (`extract_chat_completions_usage`, `extract_gemini_usage`) for callers who parse responses themselves.

I went with an opt-in mutable sink specifically to avoid touching the return type — but that's the main thing I'd want your read on.
I picked the one with the smallest default-path footprint, not necessarily the prettiest API.

## On breakage

I tried hard to make the default path a no-op, and I think it is locally:
- `usage_sink` is appended **after** `base_url` with a default, so positional calls `provider_func(prompt, model, api_key, base_url)` are unaffected; the shared `call_*` core is already keyword-only.
- Omit the sink and the request body, the network behavior, and the `list[str]` return are byte-identical (there's a test pinning this).
- Nothing bubbles into the consensus result — this deliberately stops at the provider layer (see scope below).

Treat my "non-breaking" as "non-breaking *as far as my local checkout shows*."

## Scope (deliberate)

Provider-layer only. `annotate_clusters`, `get_model_response`, and `interactive_consensus_annotation` do **not** expose or aggregate usage here. Aggregating across the many per-model/per-cluster consensus calls — and where to surface it in the result — is a separate API decision I'd rather leave to a follow-up once this low-level hook lands.

## What I've actually tested vs. not

I only have **OpenRouter and Gemini** API keys, so that's the boundary of my real world tests:

- **Validated against live APIs: OpenRouter + Gemini.** These are the two paths I actually exercised end-to-end with real keys, and they get the strongest offline tests here too.
- **Shared OpenAI-compatible core (OpenAI, DeepSeek, Qwen, Grok, StepFun, Zhipu, MiniMax):** these all route through `call_openai_compatible_api` + `extract_chat_completions_usage`, which *is* covered by offline tests and is the same path OpenRouter rides live. So the core logic is exercised — but I did **not** hit each provider's *native* endpoint with a real key. If any of them returns a non-standard `usage` shape, I wouldn't have caught it.
- **Anthropic: dropped from this PR.** Its `usage` block uses a different shape (`input_tokens`/`output_tokens`) and I can't live-validate it (no Anthropic key), so rather than ship unverified parsing I left `process_anthropic` untouched. Clean follow-up once someone can exercise it against the live API.

## Tested

Everything offline, mocking the HTTP/SDK seam — no live calls in the suite. Beyond the happy-path surfacing tests (core, `call_openai_compatible_api`, and end-to-end via `process_openai` / `process_openrouter` native-cost / `process_gemini`), I leaned on **format-drift resilience** since the whole point is to survive providers changing their payloads:

- extra/unknown `usage` fields → ignored, canonical keys still captured;
- missing `usage` block → sink stays `{}`, no `KeyError`, `list[str]` return unaffected;
- partial usage (e.g. only prompt tokens) → capture what's there, `None` (not `0`) for the rest — so "not reported" stays distinguishable from a real zero;
- malformed `usage` (non-dict / null) → `None`, no crash;
- a default-path test pinning that omitting `usage_sink` leaves request body and return byte-identical;
- an OpenRouter test asserting the `usage: {include: true}` opt-in shows up in the request body **only** when a sink is passed.

I mutation-checked the resilience tests (not just the happy path): breaking the missing-usage guard, the field normalization, the no-fabricate-total rule, the OpenRouter opt-in condition, and the Gemini field mapping each made the corresponding test fail. Full suite: 341 passed, 1 skipped (the `--run-integration` test). `ruff check` clean on the changed files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `644063c6ff93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.