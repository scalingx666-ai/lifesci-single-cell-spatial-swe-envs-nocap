# Issue

**Title:** refactor(main): move the clump-only and trim dispatch out of main()

## Description

## Problem

`main()` in `src/main.rs` was 883 lines (297–1179). It held every format guard, then the pre-flight and dispatch of every mode, all inline. The `--clump_only` branch alone was about 250 lines. The order matters here: guards must run before `ensure_output_dir` and before any write. #363, #383 and #391 all fixed checks that sat on the wrong side of that line, and the length made the order hard to see.

## Change

Three branches move into their own functions, next to the existing `run_ubam_output`:

- `run_clump_only(cli: &Cli, output_dir: Option<&Path>, gzip: bool, command_line: &str) -> Result<()>`: the whole `--clump_only` branch (FASTQ and uBAM output, SE, PE two-file, PE interleaved), including its `warn_below_clumpify_floor` call and memory parse.
- `run_paired_trim(cli, output_dir, gzip) -> Result<()>`: the two-file `--paired` FASTQ trim (cross-pair collision pre-flight, then per-pair sanity check, adapter detection and `run_paired`).
- `run_single_end_trim(cli, output_dir, gzip) -> Result<()>`: the SE trim (collision pre-flight, then the per-file loop).

The bodies are moved unchanged. The only edits are `&cli` → `cli` and `&command_line` → `command_line` (both are now references), plus the line reflows `cargo fmt` made after the dedent. `git diff --color-moved=plain --color-moved-ws=allow-indentation-change` shows nothing else.

Everything else stays in `main()`, in the same order: CLI parse and `validate`, banner, first-input sanity check, format detection, the `--phred64` / `--preserve-tags` / `--passthrough` / `--paired` / #363 / #408 guards, `ensure_output_dir`, the uBAM NOTEs, the hardtrim/clock/implicon dispatch, the `--clump_only` call, the uBAM-output and interleaved-uBAM dispatch, then the trim call. The interleaved-uBAM FASTQ branch (about 30 lines) stays inline. It is short, and it is part of the dispatch order the guards depend on.

`main()` goes from **883 to 487 lines**. Net: `1 file changed, 393 insertions(+), 382 deletions(-)` (+11 lines: three signatures, doc comments and `Ok(())` tails).

## Testing

No behaviour change. These tests cover the moved code and its guard order:

- `tests/integration_preflight_tripwire.rs`, `tests/integration_output_collision.rs`, `tests/integration_partial_output.rs` (pre-flight runs before any write, for every mode, including clump-only and SE/PE trim)
- `tests/integration_clump_only.rs`, `tests/integration_clump_only_ubam.rs`, `tests/integration_clumpify_floor_warning.rs`
- `tests/integration_paired_format_guard.rs`, `tests/integration_passthrough.rs`
- the CI `validation` job (SE and PE md5 vs Perl 0.6.11)

I also ran a release build of this branch and of `origin/dev` on the same inputs and compared the decompressed outputs. These were identical: SE trim, PE trim with `--retain_unpaired`, two-pair PE at `--cores 2`, interleaved-uBAM `--paired`, and `--clump_only` in SE/PE FASTQ and SE/PE uBAM output (BAM compared with `samtools view`).

`cargo test` (whole suite): all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output byte changes on any path.

## Suggested CHANGELOG entry

None needed: internal refactor with no user-visible change. If one is wanted, under `#### Internal`:

- **`main()` no longer inlines the clump-only and trim dispatch.** The `--clump_only`, paired-trim and single-end-trim branches moved into `run_clump_only`, `run_paired_trim` and `run_single_end_trim`; every guard and its order stay in `main()`, which shrinks from 883 to 487 lines. No behaviour change.

Part of #546 (finding 18 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0a27ba67383`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.