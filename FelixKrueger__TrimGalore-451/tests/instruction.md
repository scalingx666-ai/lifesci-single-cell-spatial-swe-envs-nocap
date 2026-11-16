# Issue

**Title:** feat(clump): name the budget on the banner and pin the memory model's constants

## Description

The `--clumpify` banner printed a predicted peak with nothing to compare it against, so the deliberate ~9% headroom read as unexplained slack; it now names the budget it came from. That removes the peak figure's own unit, so the tripwire pins the arithmetic (`930 of 1024` at the default `--memory 1G`) rather than a label. The rest of the change closes gaps in the memory model's test coverage: six hand-computed bin budgets pin the sizing across the role space, `resolved_threads` gets its first tests, and one absolute floor pin makes `MIN_BIN_BYTES` observable. Also folds in `--clump_only`'s bail naming its own mode, and qualifies the #439 CHANGELOG claim to the read lengths it actually holds for.

<details>
<summary>Detail (AI-assisted)</summary>

**Why new pins were needed.** `predicted_peak_bytes` is the algebraic inverse of `resolve_layout`, so `predicted ≤ budget` reduces to `MARGIN_NUM ≤ MARGIN_DEN` and holds for *any* coefficients. Every guard was therefore blind to σ, k, the static reservation, the FastQC charge, its cap, and the margin itself.

Perturbation matrix, each applied alone and verified to fail:

| perturbation | pin table | absolute floor pin | swept test |
|---|---|---|---|
| σ 23→20 | fail | fail | pass |
| k 64→32 | fail | fail | pass |
| static 224→512 MiB | fail | fail | pass |
| FastQC 24→0 MiB/thread | fail | ok | pass |
| cap 16→1024 threads | fail | ok | pass |
| `MIN_BIN_BYTES` **lowered** to 256 KiB | ok | fail | pass |

The swept test passing everywhere is deliberate — it is named for the two properties it does prove (the floor is the least resolvable budget; the unchecked multiplies stay inside `u64` at extreme inputs), not for coefficient drift.

**Two layers above the pins were unguarded.** `fastqc::resolved_threads` has five call sites and had zero tests, so reverting it to the plain core count would leave every pin green while the prediction stopped bounding `--fastqc_args -t N` runs. And all three floor tests were relative to the function under test, so *lowering* `MIN_BIN_BYTES` was undetectable — the last table row is that gap, closed.

**Channel depths** move behind `clump::channel_depths`, returning work and result depths together, pinned by their **sum**: `k = 4` charges for the queued batch, the batch in hand and the result slots as one quantity, so neither depth may move alone. Verified to fail when either does.

**Banner divisor.** Changing `/(1024*1024)` to `/(1000*1000)` now fails the tripwire; under the previous label-only assertion it passed.

**CHANGELOG qualification.** The claim does not hold at 25 bp: the per-bin coefficient is fitted per byte rather than per record, so a short-read library packs more records into the same bin bytes. Measured 1048–1083 MiB against a 1024 MiB budget at `--cores 2`, seven reps across two harnesses. Tracked separately; no code change here.

Verified: 790 tests pass (was 734), `cargo fmt --check` clean, `cargo clippy --all-targets --release -- -D warnings` clean.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f7b907e2c2d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.