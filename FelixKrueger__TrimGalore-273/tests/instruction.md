# Issue

**Title:** chore(release): v2.1.0 GA

## Description

## Summary

**First stable release of the Oxidized Edition.** Cuts v2.1.0 GA from beta.8.

## Changes

- `Cargo.toml`: `2.1.0-beta.8` → `2.1.0`
- `CHANGELOG.md`: GA narrative consolidating the v2.1.0-beta.1 → -beta.8 arc — Buckberry-audit performance wins (gzip level 6→1, single buffered write, Myers' bit-parallel prefilter), `--high_compression` opt-in, bundled FastQC, multi-arch container, etc. Per-beta sections retained below for full step-by-step history.
- `README.md`: drop the "Beta testing v2.1.0-beta.8" banner — `cargo install trim-galore` now installs 2.1.0 by default. Docker example: `:beta` → `:latest`. Tag-table sentence rewritten for post-GA. Rust toolchain floor bumped `1.85+` → `1.88+` (matches `Cargo.toml` `rust-version`).
- `docs/src/content/docs/install.md`: same banner removal, same `:beta` → `:latest` swap, `--version` output snippet updated to `2.1.0`.

## Headline numbers

From the [Buckberry-scale benchmarks](https://www.trimgalore.com/performance/benchmarks/) on 84M paired-end reads:

- **5.93× less CPU time at `--cores 8`** (the nf-core `process_high` default)
- **13.49× less CPU time at single-thread**
- **4.54× faster wall time at `--cores 8`** vs Perl 0.6.11 + Cutadapt 5.2

## Verification

- [x] `cargo build --release` clean (50s)
- [x] `cargo test --release` — 192/192 green
- [x] `cargo fmt --all -- --check` — clean
- [x] `cargo clippy --all-targets --release -- -D warnings` — clean
- [x] `./target/release/trim_galore --version` → `trim_galore 2.1.0 (Oxidized Edition)`
- [ ] CI green on this PR
- [ ] After merge: `gh workflow run release.yml --ref optimus_prime` to actually cut the release (push-only is gated and goes green-but-noop per the saved memory)

## After release.yml fires

- crates.io publishes `trim-galore@2.1.0`
- GHCR multi-arch image at `:v2.1.0` and `:latest`
- GitHub release `v2.1.0` with prebuilt binary tarballs for `linux-x86_64`, `linux-aarch64`, `macos-aarch64`
- Bioconda PR #65012 bumps from `2.1.0b8` → `2.1.0` (one commit on that PR)
- nf-core/rnaseq#1789 repins to the GA digest

Co-authored with [@an-altosian](https://github.com/an-altosian) (Dongze He) for the Buckberry-scale audit + Perl-parity fixes that drove the headline performance wins.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `196d84c8e989`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.