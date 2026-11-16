# Issue

**Title:** chore(dependabot): stop batching the exact-pinned crates

## Description

Three crates are exact-pinned in `Cargo.toml` with a stated reason, but only `noodles` was in the cargo `ignore` list, so the patch/minor grouping could override the other two.

#500 is what that looks like. It batched `fastqc-rust` `=1.0.1` → `=1.1.0` into the weekly group, where it fails every job — `FastQCConfig` dropped `svg_output` and `threads` became `Option<usize>`, so `src/fastqc.rs` fails with `E0308`, `E0609` and `E0277` — and it would have retargeted the bundled report at Java FastQC 0.13.0, which the validation job would not catch, since its smoke test only checks that the `.zip` contains the expected file names.

`mimalloc` is added for the same reason before it bites: allocator changes move the peak RSS that the clumpify-memory job gates on.

Neither pin is frozen, only un-batched — both still move as deliberate-test events with their own output re-verification.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da8bbd0f98fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.