# Issue

**Title:** deps: pin flate2's zlib-rs backend explicitly

## Description

Answering "are we properly setting the flate2 backend to zlib-rs": **it is active, but not by our doing.**

We declare `flate2 = "1"` with no features. The zlib-rs backend is on only transitively — `bgzip` (via niffler's default `bgz` feature, via paraseq-temp → piscem-rs) enables `flate2/zlib-rs`, and flate2 uses the zlib backend whenever `any_zlib` is on. Nothing salmon controls guarantees it.

**Why that matters for this release specifically:** if any of those upstream crates dropped the enablement, flate2 would silently fall back to `miniz_oxide` — slower, *and* it would change the bytes of every gzipped aux file (`eq_classes.txt.gz`, `bootstraps.gz`, `fld.gz`, `observed/expected_bias.gz`), because different deflate backends emit different streams. A silent perf + determinism regression with no compile error — the exact failure class 2.6.0 is built to avoid.

**The fix** declares `features = ["zlib-rs"]` on the workspace flate2 dep, making the backend ours to guarantee.

**Verified a pure no-op** (hardening only, no behavior change):
- zero `Cargo.lock` churn — zlib-rs was already resolved, so the compiled backend is bit-identical
- unified flate2 feature set unchanged
- build + fmt + clippy -D warnings clean; `cargo test --workspace --release`: **355 passed, 0 failed**
- all gzipped aux files produced and `gzip -t`-valid

rapidgzip-core already uses zlib-rs (via libz-rs-sys) for parallel *input* decompression, so the gzip read and write paths are now consistently zlib-rs. zstd is a separate codec/backend and out of scope.

Needs to land on develop before the develop→master fast-forward, so 2.6.0 ships with the backend pinned.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9caef6ee0e4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.