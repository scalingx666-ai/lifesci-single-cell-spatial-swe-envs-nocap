# Issue

**Title:** fix(fmt): hotfix rustfmt-version diff post-#250 (gzip-level imports)

## Description

Hotfix: CI's stable rustfmt and my local 1.9.0-stable disagreed on line-wrap choices around the new `OUTPUT_GZIP_LEVEL` call sites and the buffered-write `Vec::with_capacity`. Local was clean pre-merge but CI rejected post-merge ([run 25103753614](https://github.com/FelixKrueger/TrimGalore/actions/runs/25103753614)).

Two targeted fixes:
- `src/parallel.rs`: import `OUTPUT_GZIP_LEVEL` at the top so call sites are unqualified; rustfmt then naturally splits the longer `Some(GzEncoder::new(...))` expressions.
- `src/fastq.rs`: collapse the `Vec::with_capacity` into a single line.

No behaviour change. `cargo fmt`, `cargo clippy --all-targets --release -- -D warnings`, and 177 tests all clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b78a5dd3270`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.