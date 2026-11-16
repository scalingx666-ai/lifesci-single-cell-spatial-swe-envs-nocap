# Issue

**Title:** fix(map): don't construct a zero-length Mem in the radix-sort scratch fill

## Description

## Summary

`radix_sort_tidfw` (the length-dispatched `(tid, orientation)` uni-MEM grouping added in #1044) sized its ping-pong scratch buffer with:

```rust
tmp.resize(n, (0, false, Mem::new(0, 0, 0)));
```

That `Mem::new(0, 0, 0)` has `len == 0`, which violates `Mem`'s `len > 0` invariant and trips the `debug_assert!` in `Mem::new` — panicking **every debug build** the moment a read produces `>= 2` uni-MEMs to group (i.e. essentially all real reads):

```
thread '...' panicked at crates/salmon-map/src/mem.rs:30:9:
MEM length must be positive
   ...
   salmon_map::extend::radix_sort_tidfw  at extend.rs:219
```

The salmon-map unit tests never exercised the `collect → radix` path, and release builds compile the assert out, so it slipped through review and CI.

## ⚠️ Behavior-neutral — release output is unchanged

This does **not** change any quantification result:

- The scratch fill value is **never read** — the counting-sort scatter overwrites all `n` slots before the buffer is swapped, so the placeholder is pure, immediately-overwritten scratch.
- In **release** builds (what ships, and what every release regression run used) `debug_assert!` is compiled out, so the pre-fix code already behaved correctly. **Shipped 2.3.x binaries are unaffected.**
- Verified **byte-identical `quant.sf`** between the fixed *debug* build and *release* on a GEUVADIS sample (max |Δ| = 0.0 on both NumReads and TPM).

The impact of the bug was strictly that `salmon quant` built in debug mode panicked on real reads, plus the latent invariant violation.

## Fix

Fill the scratch with a copy of a real element (`flat[0]`, valid since `n >= 2`) instead of constructing an invalid `Mem`. Same size, same overwrite, no invalid `Mem` ever built.

## Test

Adds `radix_sort_tidfw_groups_by_key`, which exercises the `n >= 2` radix path (the coverage gap that let this ship) and asserts the stable `(tid, fw)` key ordering. It panics on the old code and passes on the new. `cargo test -p salmon-map` (60 tests) + `fmt` + `clippy -D warnings` clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01B7JMur5DmDpECddErpi2JS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66f3d3cdaeb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.