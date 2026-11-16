# Issue

**Title:** test(ubam): check that a failed parallel sink finish publishes nothing

## Description

and 36d2637.

This PR started as a fix for #542 with the same design as 36d2637: workers compress, the sink only appends, `PendingOutput` publishes on success, and `ParallelBamSink::create` drops its `workers` argument. Once 36d2637 landed on `dev`, I merged `dev` in and kept its implementation unchanged. What's left is one test for a case the new tests don't reach.

The tests in 36d2637 check a write error and a finish error on `BgzfSink` with injected writers (`FailingWriter`, `FlushFailsWriter`), and they check that a sink dropped without `finish` publishes nothing. None of them makes `ParallelBamSink::finish` itself fail and then looks at the disk. That path runs `BgzfSink::finish` → `?` → `PendingOutput` dropped without `commit`.

`bam::tests::parallel_sink_finish_error_publishes_nothing` (unix only):

- creates the sink's `.partial` as a FIFO whose reader has already closed, so the real `BufWriter<File>` gets `EPIPE` on the final flush;
- checks that `finish` returns the error (`failed to flush uBAM output`) instead of panicking;
- checks that neither the final `.bam` nor the `.partial` is left behind.

It would catch `pending.commit()` being moved before `inner.finish()?`, or the finish error being discarded on the real type rather than on the generic sink.

`cargo fmt --all -- --check`, `cargo clippy --all-targets --release -- -D warnings` and `cargo test --release` all pass locally.

Related upstream: zaeleus/noodles#450 makes `bgzf::io::MultithreadedWriter` return an error instead of panicking with `invalid state` after a write error. That's the part of #542 still present in the latest `noodles`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c014ca175a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.