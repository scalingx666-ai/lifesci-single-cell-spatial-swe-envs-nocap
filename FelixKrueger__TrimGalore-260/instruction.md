# Issue

**Title:** ci/test: cargo-nextest adoption + parallel.rs coverage

## Description

## Summary

Closes the two umbrella tracking issues from @an-altosian's cross-cutting audit so the GA queue is clean at 5 days out.

- **#247 #8 — `cargo nextest` adoption**: per-test-isolation audit + CI swap. 19 `temp_dir().join(...)` callsites audited (18 already used unique slugs; 1 generic slug `trim_galore_test` in `src/fastq.rs:600` renamed to `tg_fastq_round_trip`). No global mutable state in the codebase (no `static mut` / `OnceCell` / `env::set_var`). 191/191 tests pass under nextest's per-process model in 1.07 s.
- **#246 — `parallel.rs` coverage**: +3 targeted tests covering multi-member gzip output validity (producer side of the §5.1 contract), single-record-input boundary, and empty-input no-deadlock. Tests 188 → 191.
- **Drive-by**: `cargo fmt` on `src/alignment.rs:668`. CI Lint has been red on `optimus_prime` since beta.7 (commit `ef2dce3`) because the Myers'-prefilter test fixture wasn't reformatted before commit. Mechanical one-tuple reformat — Lint goes green again with this PR.

The parity-proptest harness (the §5.x bonus from @an-altosian's fork) remains "open to PR" — out of scope for the GA push at 5 days out, but a clear contribution path for whoever picks it up next. Co-authored-by trailer included for the audit work.

## Test plan

- [x] `cargo test --release` — 191/191 pass
- [x] `cargo nextest run --release` — 191/191 pass (1.07 s)
- [x] `cargo fmt --all -- --check` — clean
- [x] `cargo clippy --all-targets --release -- -D warnings` — clean
- [ ] CI `Lint (fmt + clippy)` — was red on optimus_prime, expected green here
- [ ] CI `Rust Tests (ubuntu-latest, macos-latest)` — both green under nextest

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b333ea03c01c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.