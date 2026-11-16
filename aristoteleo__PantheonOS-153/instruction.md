# Issue

**Title:** fix(catalog): stop the picker from silently serving the wrong model list

## Description

## The bug

Production's model picker intermittently collapsed to 4 models (OpenAI 2 / Anthropic 1 / Google 1), then recovered on its own a few minutes later.

Not an image update — `:prod` was last promoted 2026-07-14 and the prod hub pod had been running 16 days. It was a silent degradation at runtime:

1. `ensure_fresh()` made a single attempt; a failure only logged a warning and left `_CACHE` empty
2. `room.list_available_models` saw `is_loaded()` false and omitted `platform_models_by_provider`
3. The frontend's `Object.keys(platformApiModels).length > 0` check failed and it fell through to the BYOK default list

The cold-start failure is *known*: the warmup in `endpoint/core.py` documents that a "fresh-sandbox first outbound connection frequently fails (egress not ready yet)" and retries 8 times for it. The catalog preload sits in the same file immediately *before* that retry loop, with no retry of its own. The `_BARE_PREFIX_TO_VENDOR` comment says outright that "the sync catalog fetch has proven flaky".

## Changes

Four layers, so the cache is never empty and never misreports what it holds:

- **Backoff retries** per source. The cold-egress failure is a *fast* failure (DNS/refused), so the retries cost effectively nothing in the case they exist for.
- **Hub mirror first** (`GET /api/model-catalog`), then openrouter.ai. The Hub fetches from a long-lived process, so it is warm exactly when a cold sandbox is not. Companion PR: Nanguage/pantheon-hub#40
- **Disk cache** of the last good payload, stored **raw** so a future `_derive()` change re-derives instead of reading stale fields. Restarts start warm.
- **Bundled snapshot** in the image (`scripts/refresh_catalog_snapshot.py`, 364 models / 206KB) as the floor, so even a brand-new sandbox with no egress shows a real list.

Key tradeoff: **a fallback load deliberately does not satisfy the TTL.** Otherwise one cold start would pin a sandbox to a stale list for an hour. Retries are throttled to 60s instead.

`catalog_status()` exposes `ready`/`live`/`source`, and `room.list_available_models` forwards it to the frontend — which previously could only infer this, and inferred it wrong. Companion PR: Nanguage/pantheon-ui#28

Also warms the catalog in the ChatRoom process at setup. The endpoint process already preloaded for its own routing; the room process is the one serving the picker's RPC, and it was the one racing the cold window.

A 4xx from a source now skips the remaining retries — a Hub deployed before the mirror endpoint exists 404s, and retrying it three times just burns round-trips on the cold path. This also makes a staged rollout clean: the agent image can ship before the Hub mirror.

## Verification

`tests/test_openrouter_catalog_resilience.py`, 11 passing:

- a late retry succeeds after the first attempts fail
- no network at all falls back to the bundled snapshot
- disk cache takes precedence over the snapshot
- the Hub mirror is preferred and a successful fetch is persisted
- a failing Hub falls through to openrouter.ai
- a 404 source is not retried; a 429 source still is
- a live cache is not refetched within the TTL
- a fallback cache keeps retrying the network
- `by_vendor()` groups correctly off a fallback catalog
- an empty upstream payload never clobbers a good cache

Measured with the network stubbed out: the picker goes from the 4-model BYOK table to 15 vendor groups / 364 models.

`tests/test_model_selector.py` has 1 pre-existing failure (image-gen preference) unrelated to this change — it fails identically on `main`.

## Rollout

Needs to land on `main` to build `:latest` before staging can pick it up. Prod runs Modal pinned to `:prod` and is unaffected.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a09f4d336c4c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.