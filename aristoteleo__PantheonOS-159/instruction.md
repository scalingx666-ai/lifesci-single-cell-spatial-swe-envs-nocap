# Issue

**Title:** fix(llm): num_retries=0 meant "never call at all"

## Description

## The bug

`openai_adapter.acompletion`:

```python
retry_count = num_retries      # 0
while retry_count > 0:         # never entered
    ...                        # the request lives in here
raise APIConnectionError(f"Failed after {num_retries} retries")
```

With `num_retries=0` the loop body never runs. **No request is sent**, and the fall-through raises an error naming the network — from code that never touched it.

Measured from inside a sandbox, against a proxy that was demonstrably healthy at that moment:

```
num_retries=0 -> APIConnectionError in    1 ms     ← never called
num_retries=1 -> OK                in 3875 ms
num_retries=3 -> OK                in 2407 ms
```

One millisecond is the tell.

## How it surfaced

Every sandbox's LLM warmup has been failing since it was written, and loudly:

```
[ACOMPLETION] ✗ Call failed | Model=openrouter/deepseek/deepseek-v4-flash | Error=APIConnectionError: Failed after 0 retries
[WARMUP] attempt 1 not warm yet (APIConnectionError); retrying
[WARMUP] attempt 2 not warm yet (APIConnectionError); retrying
...through attempt 8
```

`_warmup_llm_connection` passes `num_retries=0` on purpose — *"we own the retry loop"* — so all eight attempts returned instantly, warmed nothing, and produced eight errors that read as an unreachable proxy.

The proxy was fine. From the same sandbox, at the same time:

```
DNS  pantheon-staging.aristoteleo.com  -> 2 ms
TCP  :443                              -> 21 ms
GET  /litellm/models                   -> 200 in 128 ms
GET  /litellm/health/readiness         -> 200, {"status":"healthy", ...}
POST /litellm/chat/completions         -> 200 in 1136 ms     ← same model
```

So the warmup this was meant to perform — absorbing the ~10-13 s cold model route before the user's first message — has never happened. Every user's first real message has paid it.

**Scope note.** This was found while investigating a desktop that is sluggish for its first minute on a fresh sandbox, and these failures sit in exactly that window. That is *not* evidence they cause it: each failed attempt returns in ~1 ms and then sleeps 2 s, so the loop costs single-digit milliseconds of CPU in total. It cannot be what makes an unrelated call take 0.9 s. The startup-latency question is still open and being chased separately; this PR stands on its own.

## The invisible cost

Worse than the warmup. Any caller asking for no retries — because the call is cheap, or because it owns its own retry policy, which is exactly why `_warmup_llm_connection` asked — gets a **guaranteed** failure that reads as a network fault. There is no way to make that call succeed, and nothing in the error says so.

## The fix

`retry_count = max(1, num_retries)`. Zero retries still means one attempt; every other caller's attempt count is unchanged.

The unreachable fall-through no longer claims a connection failure that never happened.

## Verified

By patching the adapter inside a running sandbox and repeating the same three calls:

```
num_retries=0 -> OK in 1319 ms     (was: APIConnectionError in 1 ms)
num_retries=1 -> OK in 1040 ms
num_retries=3 -> OK in 1330 ms
```

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a54f06ddb5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.