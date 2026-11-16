# Issue

**Title:** docs(install): Homebrew in Astro + v2.3.0 refs + clippy 1.97 unblock

## Description

(`c0328da`, merged into `dev`).

## Summary

- **Docs (Astro):** Adds a `## From Homebrew` section to `docs/src/content/docs/install.md`, mirroring the README change from #336. Live install page at https://www.trimgalore.com/install/ will be consistent with the GitHub README on next docs deploy.
- **Docs staleness fixes** (unrelated to Homebrew, folded in while touching the file):
  - Docker tag table: `currently v2.2.0` → `currently v2.3.0`
  - Pinned tag row: `:v2.2.0` → `:v2.3.0`
  - `--version` example: `trim_galore 2.1.0` → `trim_galore 2.3.0`
  - Frontmatter `description:` adds Homebrew for SEO / OpenGraph.
- **Clippy 1.97.0 unblock** (added after CI reported failure): Rust 1.97.0 promoted `clippy::byte_char_slices` — fires on `&[b'A', b'C', b'G', b'T']` form idiomatic in ACGT test scaffolding. `-D warnings` turns these into hard errors. 5 sites in `#[cfg(test)]` blocks converted to `*b"ACGT"` (byte-identical, same `u8` at every index). Unblocks CI on `dev` (broken since #336's merge — first run against Rust 1.97.0).

## Test plan

- [x] `git diff` reviewed — docs (12 lines), src (10 lines), all intentional
- [x] `cargo clippy --all-targets --release -- -D warnings` passes locally (rustc 1.95.0)
- [x] `cargo fmt --all -- --check` clean
- [ ] Full CI matrix (Rust 1.97.0 stable) passes
- [ ] Astro docs build succeeds
- [ ] Live docs at https://www.trimgalore.com/install/ show the Homebrew section after deploy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0328da683b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.