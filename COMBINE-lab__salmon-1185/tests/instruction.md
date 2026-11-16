# Issue

**Title:** deps: adopt libradicl 0.18 + hashbrown 0.17 for 2.6.0

## Description

Per @rob-p's call in the pre-2.6.0 dependency scan: adopt libradicl 0.18 (COMBINE-lab upstream, a deliberate 0.x-minor decision).

0.18 requires `noodles ^0.115`, which the tree already resolves to `0.115.0`, so **no noodles bump is forced** (the coupling that usually accompanies a libradicl bump does not bite here).

Verified against the release contract, not assumed:

- **Builds clean.** Our full RAD API surface (`chunk`/`header`/`readers`/`writers`/`record`/`rad_types`) is source-compatible; no code changes needed.
- **`cargo test --workspace --release`: 355 passed, 0 failed** (2 ignored), including all RAD round-trip and output-contract tests.
- **Determinism intact and output unchanged.** `quant.sf` is byte-identical across `-p 1/16/64` at `--sigDigits 9` on the 26M-fragment RAD, and the hash (`2a86764f…`) is **the same one the libradicl-0.17 build produced** — so 0.18 alters no quantification output.
- fmt + `clippy --workspace --all-targets -D warnings` clean.

Diff is two files: `Cargo.toml` (the pin) and `Cargo.lock` (libradicl + libradicl-macros 0.17 → 0.18). This lands before the 2.6.0 version bump.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6233d0c5d48f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.