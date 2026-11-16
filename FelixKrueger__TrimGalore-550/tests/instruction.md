# Issue

**Title:** chore(deps): drop the unused memchr and log direct dependencies

## Description

## Problem

`Cargo.toml` lists `memchr = "2"` and `log = "0.4"` under `[dependencies]`, but nothing in the crate uses them. A grep of `src/`, `tests/`, `examples/` and `build.rs` for `memchr`, `log::`, `use log` and the `log` macros (`info!`, `warn!`, `debug!`, `trace!`, `error!`) finds nothing.

## Fix

Remove the two lines from `[dependencies]`. `cargo build` updated `Cargo.lock` by itself. The only lock change is the loss of the two direct-dependency edges from `trim-galore`:

```diff
@@ -1715,8 +1715,6 @@ dependencies = [
  "fastqc-rust",
  "flate2",
  "gzp",
- "log",
- "memchr",
  "mimalloc",
  "noodles",
  "serde_json",
```

Both crates are still pulled in as transitive dependencies (by `env_logger`, `noodles`, `fastqc-rust` and others), so no crate is added, removed or re-versioned and the build graph is otherwise the same.

## A separate choice for the maintainer: `env_logger`

This PR keeps `env_logger`. No code in the crate logs anything, so `env_logger::init()` in `main.rs` only surfaces log output from dependencies (for example `noodles` or `fastqc-rust`) when a user sets `RUST_LOG`. If that is not wanted, `env_logger` and the `init()` call can go in a follow-up; if it is useful for debugging, it should stay.

## Testing

No behaviour change. `cargo fmt --all -- --check`, `cargo clippy --all-targets --release -- -D warnings` and the full `cargo test` suite pass.

## Byte-identity

No code changes, so no output byte changes on any path.

## Suggested CHANGELOG entry

- **Dropped the unused `memchr` and `log` direct dependencies.** Nothing in the crate used them; both
  remain in the tree as transitive dependencies, so `Cargo.lock` only loses the two direct edges.

Part of #546 (finding Lean / unused dependencies of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c98c98b56b96`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.