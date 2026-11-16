# Issue

**Title:** chore(deps): bump libradicl 0.20 → 0.21 (drop-noodles API + tag roles)

## Description

## Summary

Moves alevin-fry to **libradicl 0.21**, which (a) removes libradicl's `noodles` dependency and (b) ships role-aware bulk/scATAC record readers.

## Changes

- `Cargo.toml`: `libradicl` `0.20.0` → `0.21` (lockfile → 0.21.0).
- `src/convert.rs`: libradicl 0.21 replaced `RadHeader::from_bam_header(&noodles::sam::Header)` with the data-only `RadHeader::from_ref_names(...)` (). The one caller (BAM→RAD `convert`) now extracts the reference names from its own noodles header:
  ```rust
  RadHeader::from_ref_names(hdrv.reference_sequences().iter().map(|(k, _)| k.to_string()))
  ```
  alevin-fry keeps its own `noodles` dependency for BAM reading — only the libradicl API boundary changed.

## Why now

Part of the coordinated RAD v2 rollout. piscem will emit the versioned RAD v2 format unconditionally; a **published** alevin-fry must be on libradicl ≥ 0.20 to read it (the currently-published 0.18.3 pins libradicl 0.19.1 and would misread v2). Moving to 0.21 (rather than 0.20) unifies the ecosystem on one libradicl and picks up the role-driven readers, so v2 role-annotated files are parsed via their declared tag roles (name-bridge fallback for legacy files). This unblocks cutting **alevin-fry 0.19.0**.

## Validation

`cargo build` / `cargo test` green (71 unit + integration suites pass); `cargo fmt --check` clean; `cargo clippy --all-targets` clean. Builds against the published libradicl 0.21.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7c882aff1469`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.