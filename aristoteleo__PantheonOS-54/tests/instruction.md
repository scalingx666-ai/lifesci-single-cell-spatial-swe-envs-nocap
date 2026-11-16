# Issue

**Title:** feat: CC-aligned token optimization pipeline (5-stage)

## Description

## Summary

Implements a comprehensive 5-stage token optimization pipeline in PantheonOS.

## What Changed

### 1. Tool Result Budget (`token_optimization.py`)
- **Per-tool size thresholds**: `PER_TOOL_RESULT_SIZE_CHARS` dict (grep=20K, glob=10K, shell=50K, read_file=40K). Default fallback lowered to 50K matching CC's `DEFAULT_MAX_RESULT_SIZE_CHARS`.
- **querySource filtering**: `_should_persist_to_disk()` skips disk writes for `agent_summary`/`memory_agent`/`title_agent`.
- **Session resume reconstruction**: `reconstruct_content_replacement_state()` rebuilds state from message history on resume.
- **Infinity opt-out**: `PERSISTENCE_OPT_OUT_TOOLS` frozenset for tools that should never be externalized.
- **Empty result guard**: `guard_empty_tool_results()` injects `[No output]` placeholder.
- **JSON content-type detection**: Writes `.json` for JSON arrays/objects, `.txt` otherwise.

### 2. Micro-Compact (`token_optimization.py`)
- **Time-based clearing**: 60min gap threshold, keeps last 5 compactable tool results.
- **HISTORY_SNIP**: `snip_messages_to_budget()` — drops oldest messages to fit token budget (80K default, keep 6 recent). Runs BEFORE microcompact.

### 3. Cache Stability (`token_optimization.py`, `agent.py`)
- **cache_control injection**: `inject_cache_control_markers()` adds `{"type": "ephemeral"}` on system + last user/assistant message. Anthropic-only via `is_anthropic_model()`.
- **skip_cache_write**: For fork queries, marker shifts to second-to-last message.
- **Tool definition stabilization**: `stabilize_tool_definitions()` ensures deterministic ordering.

### 4. LLM View Layer (`token_optimization.py`)
- **5-stage pipeline**: budget → snip → microcompact → **contextCollapse** → **autocompact**
- **contextCollapse** (NEW): Folds consecutive read/search/bash tool sequences into compact summaries like `[Collapsed exploration: searched 5 patterns, read 3 files]`.
- **autocompact** (NEW): Last-resort summarization when still over budget after all prior stages.

### 5. Delegation (`team/pantheon.py`)
- **Restructured to fork-first** (CC's `forkContextMessages`):
  - Path 1 (primary): Cache-compatible fork — share parent prefix byte-for-byte
  - Path 2: Structured fork — pass optimized parent history as structured messages
  - Path 3 (fallback): Summary — only when no structured context available

---

## Benchmark Results — Per-Optimization Token Savings

### Opt 1: Tool Result Budget (externalize large outputs to disk)

Each tool result exceeding its per-tool threshold is replaced by a stable preview + file reference. Session-level: once externalized, every subsequent turn reuses the preview.

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,794 | 12,794 | 0 | 0.0% |
| Medium (10×50KB) | 128,083 | 5,381 | 122,702 | **95.8%** |
| Large (20×100KB) | 512,016 | 10,711 | 501,305 | **97.9%** |
| XL (30×200KB) | 1,535,712 | 16,039 | 1,519,673 | **99.0%** |

> Small shows 0% because each 10KB tool result is below the per-tool threshold (shell=50K). At Medium scale (50KB/result), shell results exceed the 50K limit and get externalized.

### Opt 2: Micro-Compact (time-based clearing of old tool results)

Clears compactable tool results older than the gap threshold (60min), keeping only the most recent N results.

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,794 | 5,199 | 7,595 | **59.4%** |
| Medium (10×50KB) | 128,083 | 25,787 | 102,296 | **79.9%** |
| Large (20×100KB) | 512,016 | 51,536 | 460,480 | **89.9%** |
| XL (30×200KB) | 1,535,712 | 102,875 | 1,432,837 | **93.3%** |

> Consistent savings across all scales. The kept-recent count (2 in benchmark) determines the floor.

### Opt 3: Cache Stability — Live API Cache Hit Test (gpt-4.1-mini)

Test method: Build a long conversation (~1,345 prompt tokens with 5 tool definitions). Send the same request twice in sequence, measure `prompt_tokens_details.cached_tokens` on each call. Compare unstable (tool order shuffled between calls) vs stable (`stabilize_tool_definitions()`).

| Group | Call | prompt_tokens | cached_tokens | Hit Rate |
|-------|------|---------------|---------------|----------|
| Unstable order | call1 (warm-up, order_a) | 1,345 | 0 | 0.0% |
| Unstable order | call2 (order_b, shuffled) | 1,345 | 0 | 0.0% |
| Stable order | call1 (warm-up, sorted) | 1,345 | 1,280 | **95.2%** |
| Stable order | call2 (sorted, same) | 1,345 | 0 | 0.0% |

- Stable call1 achieved **95.2% cache hit** (1,280/1,345 tokens) — reused the prefix cached from prior unstable call1 (same `order_a`). Stable ordering preserved this cache.
- Unstable call2 got **0%** because tool order changed to `order_b`, invalidating the entire prefix.
- OpenAI automatic caching has variable warm-up timing. Key takeaway: **stable tool ordering is a prerequisite for cache reuse** — any reordering forces full re-evaluation.
- For Anthropic API: `inject_cache_control_markers()` adds explicit `cache_control: {"type": "ephemeral"}` markers, which is **required** for Anthropic to cache (OpenAI caches automatically without markers).

### Opt 4a: HISTORY_SNIP (token-budget truncation)

Drops oldest non-system messages until total tokens fit within budget (20K in benchmark). Protects last N messages (4 in benchmark).

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,794 | 12,794 | 0 | 0.0% |
| Medium (10×50KB) | 128,083 | 12,835 | 115,248 | **90.0%** |
| Large (20×100KB) | 512,016 | 25,631 | 486,385 | **95.0%** |
| XL (30×200KB) | 1,535,712 | 51,221 | 1,484,491 | **96.7%** |

> Small is under budget (12K < 20K) so no snipping occurs.

### Opt 4b: contextCollapse (read/search group folding)

Identifies consecutive collapsible tool-use sequences (grep, read_file, glob, shell, web_fetch with silent assistant messages), groups them, and replaces each group with a single compact summary message.

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,722 | 78 | 12,644 | **99.4%** |
| Medium (10×50KB) | 127,975 | 78 | 127,897 | **99.9%** |
| Large (20×100KB) | 511,832 | 78 | 511,754 | **100.0%** |
| XL (30×200KB) | 1,535,452 | 79 | 1,535,373 | **100.0%** |

> Tested with `build_collapsible_conversation()` — assistant messages contain ONLY `tool_calls` (no text), simulating real exploration sequences where the model silently chains searches. The entire exploration chain collapses to ~78 tokens regardless of scale.

### Opt 4c: Autocompact (last-resort summarization)

When total tokens exceed budget after all prior stages, replaces oldest messages with a compact text summary preserving key information.

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,794 | 12,794 | 0 | 0.0% |
| Medium (10×50KB) | 128,083 | 13,662 | 114,421 | **89.3%** |
| Large (20×100KB) | 512,016 | 26,912 | 485,104 | **94.7%** |
| XL (30×200KB) | 1,535,712 | 52,503 | 1,483,209 | **96.6%** |

> Small is under budget so autocompact does not trigger. At larger scales, older messages are summarized into ~300 chars each, capped at 30 entries.

### Opt 4 Combined: Full LLM View Layer (5-stage pipeline)

All stages chained: budget → snip → microcompact → contextCollapse → autocompact.

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,794 | 12,794 | 0 | 0.0% |
| Medium (10×50KB) | 128,083 | 5,381 | 122,702 | **95.8%** |
| Large (20×100KB) | 512,016 | 10,711 | 501,305 | **97.9%** |
| XL (30×200KB) | 1,535,712 | 16,039 | 1,519,673 | **99.0%** |

> The pipeline stages are complementary — budget handles large individual results, snip handles over-budget history, microcompact clears stale results, collapse folds exploration chains, autocompact summarizes whatever remains.

### Opt 5: Delegation (fork-first vs full history)

Compares what a sub-agent receives: full parent history (before) vs compact delegation context (after).

| Scale | Raw Tokens | After | Saved | % |
|-------|-----------|-------|-------|---|
| Small (5×10KB) | 12,814 | 778 | 12,036 | **93.9%** |
| Medium (10×50KB) | 128,103 | 1,051 | 127,052 | **99.2%** |
| Large (20×100KB) | 512,036 | 1,052 | 510,984 | **99.8%** |
| XL (30×200KB) | 1,535,732 | 1,052 | 1,534,680 | **99.9%** |

> The delegation context message (summary + recent tail of 20 messages + file references + task instruction) is ~1K tokens regardless of parent history size.

### Live API Verification (gpt-4.1-mini, real `prompt_tokens`)

Combined pipeline (Opt 1+2+4) measured against OpenAI's actual token counter:

| Scenario | Before (API) | After (API) | Saved | % |
|----------|-------------|------------|-------|---|
| 5×30KB | 49,578 | 21,320 | 28,258 | **57.0%** |
| 10×50KB | 165,512 | 7,272 | 158,240 | **95.6%** |
| 15×80KB | 397,066 | 10,816 | 386,250 | **97.3%** |

---

## How The Benchmark Works

1. **Synthetic conversations**: `build_conversation(rounds, output_kb)` creates N rounds of tool calls (shell, read_file, grep, web_fetch, bash) with configurable output sizes. Timestamps are set to 2 hours ago to trigger time-based microcompact.

2. **Isolation testing**: Each optimization is measured independently — the same raw conversation passes through ONLY that one stage, so savings are attributable to a single mechanism.

3. **Token estimation**: Local tests use `len(content) // 4` (4 bytes = 1 token). Live tests read `response.usage.prompt_tokens` from gpt-4.1-mini API responses.

4. **contextCollapse testing**: Uses `build_collapsible_conversation()` with silent assistant messages (tool_calls only, no text content) to simulate real exploration sequences that trigger the collapse logic.

5. **Live API method**: Tool messages are flattened into user messages (preserving token count) since OpenAI requires matched tool_call/tool pairs. Sent with `max_completion_tokens=1` to minimize cost.

6. **Cache test**: Same conversation+tools sent twice — once with randomized tool order, once with `stabilize_tool_definitions()`. Measures `prompt_tokens_details.cached_tokens` on second call.

## Not Implemented (Anthropic-proprietary)

| Feature | Reason |
|---------|--------|
| CACHED_MICROCOMPACT (`cache_edits` API) | Anthropic-native KV cache editing, requires proprietary API |
| 1h TTL / global/org cache scope | Anthropic account-level feature, GrowthBook-gated |
| Cache break detection + BQ analytics | Observability infrastructure, not algorithm |

These are platform dependencies, not algorithm gaps. PantheonOS uses LiteLLM for multi-provider routing.

## Test Plan

- [x] 52/52 unit tests passing
- [x] Tool Result Budget: per-tool thresholds, opt-out, empty guard, JSON detection, querySource filtering, session resume
- [x] Micro-Compact: time-based clearing, HISTORY_SNIP budget truncation
- [x] Cache Stability: marker injection, skip_cache_write, model detection, idempotency
- [x] LLM View Layer: contextCollapse folding, autocompact summarization, full 5-stage pipeline
- [x] Delegation: structured fork, cache-compatible fork, summary fallback
- [x] Benchmark: local estimation + live OpenAI API verification

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ba9a902b64db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.