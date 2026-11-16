# Issue

**Title:** refactor(cli): move the global allocator into its own module, document the gates for changing it

## Description

## What this is now

Scoped down to the half you said you'd take: the allocator placement, plus the
documentation of what would gate changing it. No new dependency, no new feature,
no behavior change.

* `#[global_allocator]` moves out of `main.rs` into
  `crates/salmon-cli/src/global_alloc.rs`, alongside a `NAME` constant reporting
  which allocator a build actually got. The binary logs it at `debug`.
* `examples/cache_bench.rs` pulls that same file in via `#[path]`, so the
  microbenchmark and the real binary cannot disagree about what is in play.
* mimalloc stays the default; `sysalloc` stays the diagnostic escape hatch it
  already was on `master`. `Cargo.lock` is back to `master`'s.

Dropped from the previous revision: the `jemalloc` and `snmalloc` features and
their dependencies.

## The documentation half

`docs/allocator-choice.md` now leads with the negative result rather than the
microbenchmark, and states the bar rather than implying the features were their
own justification. It records:

1. **The gates.** An end-to-end win on a real quant run (faster wall clock
   without a non-trivial RSS increase, or the same wall clock with a
   considerable RSS decrease), and evidence that the win holds across the
   input, output and option surfaces (selective alignment and sketch, with and
   without decoys, with and without mapping output, across a realistic `-p`
   range). Plus the supporting discipline: interleaved arms, spread reported
   with the median, `quant.sf` hashed to prove the arms compute the same thing.
   It notes #1126 and #1041 as the same bar applied elsewhere.

2. **The measurement behind the current default**, which was already in the
   file and which agrees with you: a four-way end-to-end round (GENCODE v50,
   10M pairs, `-p 16`, 5 interleaved reps) where system malloc is +38% on the
   mapping phase, jemalloc is ~7% behind mimalloc, and snmalloc is inside the
   noise floor while costing ~0.4 GiB more peak RSS. Nothing there justifies a
   switch. The doc now also says explicitly what that round does *not*
   establish under gate 2: one machine, one reference, one simulated read set,
   one option configuration.

3. **The two traps**, since both produced confident wrong answers first: the
   single-threaded microbenchmark ranks the four allocators in an order the real
   workload contradicts, and a cold-page-cache first round produced the exact
   reverse of the settled ranking.

## Verification

`cargo fmt --all --check` clean. `cargo build -p salmon-cli --all-targets`
clean, and clean again with `--features sysalloc`.
`cargo clippy -p salmon-cli --all-targets` clean (the only remaining note is the
pre-existing future-incompat warning from the third-party `proc-macro-error2`).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbda523f627d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.