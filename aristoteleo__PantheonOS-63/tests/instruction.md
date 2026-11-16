# Issue

**Title:** feat: CC-aligned token optimization with multi-provider cache support

## Description

## Summary

Re-integrates the 5-stage CC-aligned token optimization pipeline (from PR #54 and #57) on top of main's litellm-free architecture, with new multi-provider cache support.

### What's included

1. **Token optimization pipeline restored and adapted** — all 5 stages working without litellm:
   - Stage 1: Tool Result Budget (externalize large outputs to disk)
   - Stage 2: History Snip (drop oldest messages over token budget)
   - Stage 3: Time-Based Microcompact (clear old compactable tool results)
   - Stage 4: Context Collapse (fold consecutive read/search groups)
   - Stage 5: Autocompact (LLM-based summarization, adapted to use `acompletion` with `model_params`)

2. **Cache control extended to Qwen** — new `supports_explicit_cache_control()` function enables `cache_control: {"type": "ephemeral"}` injection for both Anthropic and Qwen models (same format).

3. **Multi-provider benchmark** — new `scripts/benchmark_multi_provider.py` tests token reduction + cache behavior across 6 providers.

### Benchmark Results

#### Local Token Optimization (provider-independent)

| Optimization | Medium (128K tok) | Large (512K tok) |
|---|---|---|
| Micro-Compact | **79.9%** | **89.9%** |
| HISTORY_SNIP | **90.0%** | **95.0%** |
| contextCollapse | **100.0%** | **100.0%** |
| Full Pipeline | 50.0% | 85.0% |
| **ALL COMBINED** | **79.9%** | **90.0%** |

#### Live API Token Reduction (10x50KB scenario)

| Provider | Model | Raw | Optimized | Saved |
|---|---|---|---|---|
| OpenAI | gpt-4.1-mini | 170,827 | 34,287 | **79.9%** |
| Gemini | gemini-2.5-flash | 248,316 | 49,757 | **80.0%** |
| Kimi | kimi-k2.5 | 170,849 | 34,301 | **79.9%** |

#### Cache Hit Comparison

| Provider | Unstable c2 | Stable c2 | Cache Type |
|---|---|---|---|
| **DeepSeek** | 448 | **448** | Auto disk (64-token granularity) |
| **Kimi** | 0 | **588** | Auto prefix (stable ordering required!) |
| OpenAI | 0 | 0 | Auto prefix (needs longer warmup) |
| Gemini | 0 | 0 | Implicit auto (no guarantee) |

Key finding: `stabilize_tool_definitions()` is critical for Kimi — unstable tool ordering = 0 cache hits, stable ordering = 588 cached tokens.

#### Cache Strategy Per Provider

| Provider | Explicit Markers | Strategy |
|---|---|---|
| OpenAI | No | Auto prefix — stable tool definitions help |
| **Anthropic** | **Yes** | `cache_control` markers injected |
| Gemini | No | Implicit auto — stable prefixes help |
| DeepSeek | No | Auto disk — 64-token granularity |
| **Qwen** | **Yes (NEW)** | Same `cache_control` format as Anthropic |
| Kimi | No | Auto prefix — `stabilize_tool_definitions` verified |

### litellm Adaptation

- `acompletion_litellm` → `acompletion` (unified adapter-based routing)
- `max_tokens`/`temperature` → `model_params` dict (new `acompletion` signature)
- Removed litellm version check in `inject_cache_control_markers` (native SDK handles it)
- `is_anthropic_model` check → `supports_explicit_cache_control` (Anthropic + Qwen)

### Files Changed

- `pantheon/agent.py` — AgentRunContext cache fields, build_llm_view_async pipeline, cache marker injection
- `pantheon/utils/token_optimization.py` — all 5 stages + litellm-free adaptations + Qwen support
- `pantheon/team/pantheon.py` — delegation cache helpers and structured fork context
- `pantheon/utils/llm.py` — per-tool limits in process_tool_result
- `pantheon/utils/truncate.py` — persisted-output format
- `pantheon/settings.py` — max_tool_content_length (50K), max_file_read_chars (500K)
- `pantheon/toolsets/python/python_interpreter.py` — shared_executor support
- `scripts/benchmark_multi_provider.py` — NEW: 6-provider benchmark
- `scripts/benchmark_token_optimization_live.py` — live API optimization test
- `tests/test_token_optimization.py` — 65 unit tests (all mocked, no API keys needed)

## Test plan

- [ ] `pytest tests/test_token_optimization.py` — all 65 tests pass (no API keys needed)
- [ ] `pytest tests/test_truncate.py` — truncation tests pass
- [ ] Run `scripts/benchmark_multi_provider.py` with API keys to verify live token reduction
- [ ] Run `scripts/benchmark_token_optimizations.py` for full per-optimization breakdown

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57f626780dd1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.