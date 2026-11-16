# Issue

**Title:** refactor: share the hardtrim clip and the clump bin types

## Description

## Problem

Two pieces of logic existed as hand-kept copies:

- **Hardtrim clip-and-rename** was written out four times in `src/specialty.rs`: `hardtrim5`, `hardtrim3`, `hardtrim5_to_bam`, `hardtrim3_to_bam`. Each had the same `if record.seq.len() > keep { if rename { append :clip5:/:clip3: } truncate / clip_5prime }` body.
- **`SingleBin` / `PairedBin`** (the per-bin buffers of the `--clumpify` and `--clump_only` dispatchers) were defined in both `src/parallel.rs` and `src/clump_only.rs`. The prev-cycle reservation fix had to be applied to both copies, and each file carried its own test of the same rule.

I compared the two bin copies line by line. The fields, `with_budget`, `push` (including the `prev_mean_bytes` fallback and the `predicted + predicted / 16 + 1` headroom), `is_empty` and `take` are the same. Only the comments differ: the `parallel.rs` copy had the fuller rationale. So they were merged.

## Change

- `specialty.rs`: one private `fn apply_hardtrim(record: &mut FastqRecord, keep: usize, end: HardtrimEnd, rename: bool)`, reusing the existing `HardtrimEnd` enum. All four loops call it. Reader/writer setup in each function is unchanged.
- `clump.rs`: `SingleBin` and `PairedBin` now live here as `pub(crate)` (moved from `parallel.rs`, keeping its comments). `records`, `r1` and `raw_bytes` are `pub(crate)` because the `clump_only.rs` dispatch loops read them for occupancy and the flush check; everything else stays private. The four `clump_only.rs` dispatch loops are untouched apart from the import.
- Tests: the three bin tests in `parallel.rs` (`bin_reservation_follows_the_previous_cycle_not_one_short_record`, `single_bin_reservation_follows_the_previous_cycle`, `bin_reservation_falls_back_to_the_first_record_before_any_cycle`) moved to `clump.rs` with the types. The two copies in `clump_only.rs` (`single_bin_reservation_follows_the_previous_cycle`, `paired_bin_reservation_follows_the_previous_cycle`) were removed: they tested the same rule, with weaker assertions, on what is now the same type.

Net: `4 files changed, 220 insertions(+), 372 deletions(-)` (−152 lines).

## Testing

No behaviour change. The existing suite covers the moved code:

- Hardtrim: `tests/integration_output_collision.rs` (`hardtrim{5,3}_*`, `hardtrim{5,3}_ubam_*`), `tests/integration_preflight_tripwire.rs` (`hardtrim5_fastq`, `hardtrim5_ubam`, `hardtrim3_fastq`, `hardtrim3_ubam`), `tests/integration_partial_output.rs`, `tests/integration_ubam_out.rs`, and the CI `validation` job (hardtrim5 md5 vs Perl 0.6.11).
- Bins: the three moved unit tests in `clump::tests`, plus `tests/integration_clump_only.rs`, `tests/integration_clump_only_ubam.rs`, `tests/integration_clumpify_floor_warning.rs` and the `parallel.rs` clumpify parity tests.

No test pins the `--rename` header content, so I also ran a release build of this branch and of `origin/dev` on the same inputs and compared the decompressed outputs:

- `--hardtrim5 20 --rename` and `--hardtrim3 20 --rename` on `BS-seq_10K_R{1,2}.fastq.gz`: identical.
- `--hardtrim{5,3} 20 --rename --output-format ubam` on the nine `test_files/*.bam` fixtures that accept it: identical records (`samtools view`; the `@PG CL:` line differs only by binary path). The five whitespace/LF-qname fixtures are refused by both builds with the same error.
- `--clump_only --cores 2` SE and PE, `--clumpify --cores 2` SE and PE on the BS-seq pair: identical.

`cargo test` (whole suite): all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

## Byte-identity

No output byte changes on any path, including the Perl-validated hardtrim5 path.

## Suggested CHANGELOG entry

None needed: internal refactor with no user-visible change. If one is wanted, under `#### Internal`:

- **The hardtrim clip and the clump bin buffers are each defined once.** `--hardtrim5`/`--hardtrim3` (FASTQ and uBAM output) share one `apply_hardtrim`, and `SingleBin`/`PairedBin` moved into `clump.rs` for both `--clumpify` and `--clump_only`. No behaviour change.

Part of #546 (finding 17 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0a27ba67383`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.