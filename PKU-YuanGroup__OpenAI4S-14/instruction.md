# Issue

**Title:** fix: harden the ReAct tool surface, env pinning, and turn-completion semantics

## Description

Fixes six joint-surface defects between the ReAct tool layer, the gateway turn loop, the environment pin, and the live Notebook — plus one documentation drift. Each is one commit, with a regression test that fails on the parent commit.

## Commits

| commit | fix |
|---|---|
| `04ad113` | Fence scanning becomes nesting-aware and code-wins |
| `8525c29` | Tool calls truly never raise; 20k/60k become strict limits |
| `7961701` | Close three bypasses in the dangerous-bash precheck |
| `95c25d8` | Only `host.submit_output(...)` may complete a turn |
| `412b150` | A pinned env stays recoverable after a base fallback |
| `5b59948` | Live Notebook cells come from the server's cell-start event |
| `25c3c7b` | `kernel/install` is not REPL-gated (doc drift) |
| `94746c3` | Eliminate exponential backtracking introduced by `7961701` |

## What was actually broken

**Fence parsing truncated real work.** The old parser paired ` ``` ` delimiters top-to-bottom with a regex, so a literal ` ```tool ` example quoted inside a ` ```python ` cell (the agent writing docs about this very syntax) cut the cell short. An unclosed fence still parsed as an executable action. A single shared scanner now tracks a delimiter stack by fence character and run length; longer backtick runs and tilde fences isolate an inner triple-backtick example, and only complete top-level blocks are executable. `_extract_code`, `parse_tool_calls`, `_ProseStreamer`, and the batched-cell warning all route through it, so the live prose stream and the persisted bubble can no longer diverge.

**"Never raises" was only true for the dispatch call.** A non-dict call, a non-dict `arguments`, or a mapping whose `.get` throws escaped `execute_tool_call` and killed the turn loop. Deep JSON escaped `_parse_tool_body`, which caught `ValueError`/`TypeError` while the decoder raises `RecursionError`.

**The limits were not limits.** Truncation sliced to the limit and *then* appended a marker, pushing the result past it. Worse, a single large result could push the "N further tool call(s) were NOT run" notice past the truncation boundary, hiding from the model that its later calls never ran. Control-plane notices now come first.

**Prose could complete a task.** `docs/architecture.md` states a task ends only when the agent calls `host.submit_output(...)`. The gateway did not enforce that: a prose-only reply ended the turn as `completed` once an LLM `conclusion_gate` judged it actionable — and the gate failed open, so a slow or broken gate call silently became "this turn is done". Prose is now never a completion signal; exhausting the turn limit without a structured submit fails the turn explicitly. Plan-mode preview replies remain a non-executing exception.

**A pinned env could never come back.** `SessionState` conflated "the env the kernel runs in" with "the env the user pinned". When a pin was momentarily undiscoverable, the spawn fell back to base and wrote base into `env_name`. The DB pin survived, but the live session never retried, and `restart_kernel` took the `Kernel.restart()` path — reusing the base interpreter forever. Split into `desired_env` / `env_name`.

**Live Notebook cells were reconstructed by scraping.** The UI regexed `cell N` out of the echoed tool label, read `kernel_id` from an async status cache that could race the first cell, and hardcoded `language`. A prose heading that merely matched a tool name (e.g. `read_file`) was misclassified as a non-code tool. The server now carries `cell_index`, canonical `kernel_id`, and `language` on the cell-start event.

**The bash precheck could be hung by the input it screens.** CodeQL caught this one *on this PR*: the hardened `rm` pattern in `7961701` let a bare `--` token parse two ways, so n repeated tokens had 2^n parses and a failing match tried them all. An 83-character command took 3.3 seconds, doubling per added token — a way to hang the safety gate itself with untrusted model output. `94746c3` gives every option token exactly one parse; the same input now takes 0.013ms and scales linearly.

## Verification

- `uv run pytest` — full offline suite passes (1 pre-existing skip)
- `uv run pre-commit run` — clean on every changed file
- `node --check app.js` — passes
- Every commit passes the full suite independently. Note that `7961701` alone carries the ReDoS that `94746c3` removes, so a `git bisect` landing exactly there hits a slow-regex (not a correctness) defect.

## Not done

The `app.js` and gateway streaming changes were **not driven end-to-end in a real browser**, which `CLAUDE.md` asks for on web-UI changes; only `node --check` plus server-side unit tests. No browser runtime instance was available.

Follow-up, deliberately left out of scope: `conclusion_gate` in `openai4s/prompts.py` is now dead code — `95c25d8` removed its only caller.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `261bbbbb11e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.