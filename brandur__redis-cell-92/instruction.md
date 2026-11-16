# Issue

**Title:** Don't abort the server when a limiter key holds a non-integer value

## Description

.

`get_with_time` called `.unwrap()` when parsing the stored theoretical arrival time. `Throttle_RedisCommand` is an `extern "C"` entry point, so that panic is non-unwinding and aborts the whole server process rather than failing the single command.

Two commands from any client were enough:

```
SET mykey hello
CL.THROTTLE mykey 15 30 60 1
```

Reproduced on Redis 8.10.1 (exit 133) and Valkey 9.1.2 (exit 134), both with `crashed by signal: 6` and a backtrace through `Throttle_RedisCommand`.

An empty value hits the same path, which is the race `compare_and_swap_with_ttl` already guards against a few lines above — *"the key's already been expired even since the beginning of this operation"* — but `get_with_time` never got the matching guard.

**This change:** empty reads as a cold key, matching the CAS path; a present-but-unparseable value returns a command error.

One file, 19 lines. `cargo test`, `cargo clippy -- -D warnings` and `cargo fmt --check` all pass.

No test is included here because the existing suite exercises `MemoryStore`, a typed `HashMap<String, u64>` that cannot represent the bad state, and CI has no live Redis to load the module into. Verified manually against both engines with the repro above, plus negative and float values. Happy to add a Redis-backed integration test if you would like CI extended for it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d4233870d3c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.