# Issue

**Title:** fix(cli): apply the -p cap to mapping threads, not only the rayon pool

## Description

## Problem

`run_quant` caps `-p` at the machine's hardware threads and warns "using N". The capped value only reaches the global rayon pool, used by the EM and bias passes. Mapping reads `args.threads`, so it still spawns the requested number.

Measured on a 16-thread machine with `-p 100000`, using `threads` in `cmd_info.json`, which records the value mapping is given:

| | log says | mapping gets |
|---|---|---|
| before | using 16 | 100000 |
| after | using 16 | 16 |

The guard's own comment names the case: an unset scheduler variable or a mistyped digit. That case still oversubscribed the node.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit noticed that the capped `nthreads` is never assigned to the quant options, then confirmed it by running `-p 5000` and reading the mapping thread count from the log. Tracked in #1283 (finding 13).

## Fix

`opts.num_threads` takes the capped value. `0` stays `0`, because it already means "all cores" further down.

## Behaviour change

`cmd_info.json` now records the capped thread count rather than the requested one when `-p` is too large.

## Verification

- New test `an_oversized_thread_count_is_capped_for_mapping_too` in `crates/salmon-cli/tests/input_validation.rs`. I saw it fail without the fix (`100000` versus `16`).
- `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.