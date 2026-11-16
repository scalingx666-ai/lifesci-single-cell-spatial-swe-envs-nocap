# Issue

**Title:** fix(io): drop the local mem::forget now that gzp 2.0.3 disarms its own Drop

## Description

Rebase of #479 by @sujeito-operator onto current `dev`, with the comment blocks trimmed.

`Sink::finish`'s `--cores N` arm carried a local `std::mem::forget(w)`. gzp 2.0.2's `ParCompress::finish` propagated a failed `flush_last` with `?` before taking its channels and join handle, so `Drop` saw all three still `Some`, called `finish()` again and unwrapped the same error — turning a reportable I/O failure into a panic, which is what #434 set out to remove. Disarming that `Drop` leaked a `Sender` pair and a `JoinHandle` and left the compressor threads parked on a channel that never closed. gzp 2.0.3 routes error paths through `recover_send_error`, which takes the handle and drops the senders, so the threads exit and `?` can be used directly. The `gzp` floor moves to 2.0.3 for that reason.

Only the CHANGELOG conflicted on the rebase; `Cargo.toml`, `Cargo.lock` and `src/fastq.rs` applied unchanged. I trimmed the two new comment blocks from 35 added lines to 9 — they described the old code rather than the current invariant, which is the house rule. 824 tests pass, both `pargz_sink_finish_*` tests green, cold clippy and `fmt` clean.

Verified when I first reviewed #479: the 2.0.3 floor is load-bearing — on 2.0.2 with the `mem::forget` removed, `pargz_sink_finish_reports_a_failing_teardown_without_panicking` genuinely panics rather than fails.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `630315276ce1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.