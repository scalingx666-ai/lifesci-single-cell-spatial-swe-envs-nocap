# Issue

**Title:** fix(collate): trip gather-failed flag on worker panic; review cleanups

## Description

Non-blocking follow-ups surfaced by the pre-merge reviews of #195 / #196 (both now merged to develop).

## Changes
- **Panic-hang fix (the important one).** The collation gather producer busy-waits on a bounded queue and stops only when a shared `gather_failed: AtomicBool` is set. Previously only an `Err` *return* set it; a worker that **panicked** unwound without setting it, so at the 2-thread floor (a single gather worker) the producer could spin on a full queue forever. Added `utils::FailFlagGuard`, an RAII guard held at the top of each worker (scRNA `collate.rs` + scATAC `atac/collate.rs`): disarmed only on a clean `Ok`, so an `Err` return **or a panic** leaves it armed and its `Drop` trips the flag; the thread boundary still surfaces the panic via `join()`. Unit-tested, incl. the panic-while-armed case.
- **Debug assertion** in `correct_umis_cellranger` that UMIs carry no bits above `2*umi_len` (relied on by the radix key packing and the all-pairs popcount).
- **Docs:** note the `--small-thresh` / `--umi-edit-dist` interaction in `quant.rst`.
- **Comment cleanup:** removed review-process narrative (external branch/commit refs, "advisor item" notes) from `main.rs`, `quant.rs`, `pugutils.rs`.

No behavior change on the success path.

## Verification
`cargo fmt --check`, `cargo clippy --all-targets --features dev-tools -- -D warnings`, `RUSTDOCFLAGS=-D warnings cargo doc --workspace --no-deps`, `cargo build --release`, and `cargo test` / `cargo test --features dev-tools` all pass (incl. the new `fail_flag_guard_tests`).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0bc3c887f6a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.