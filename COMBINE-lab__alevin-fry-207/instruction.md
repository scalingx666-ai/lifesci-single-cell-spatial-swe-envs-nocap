# Issue

**Title:** fix: return errors instead of aborting on bad input (RAD header, view, USA quant, knee, ATAC)

## Description

## Summary

Release builds set `panic = "abort"`, so when a user-input check is an `unwrap`, `expect` or `assert`, a bad input ends in SIGABRT (exit 134) with a "panicked at" frame and a core dump. This PR turns the user-reachable cases found in the RAD v2 evaluation into contextual errors that exit 1. It also fixes two cases that are not crashes:

- a multi-sample knee run used to die on 1–2-barcode samples; it now completes;
- a scATAC permit list that keeps no barcode used to "succeed" and produce an empty BED; it is now an error.

Successful runs produce the same output as before. Among other things, this fixes the USA-mode bootstrap abort reported in issue #157, which was closed without a fix.

## Changes

- **Unreadable RAD input.** This covers a too-new spec major, a truncated file and an empty file.
  - `generate-permit-list` reads the prelude and tags with `?` and context naming `map.rad`.
  - `atac generate-permit-list` uses `ParallelRadReader::try_new`.
  - `atac deduplicate` and the quant tag map use `?`.
  - `collate`, `atac collate`, `atac sort`, `atac deduplicate` and `infer` propagate errors from `main`/`atac::run` instead of `.expect()` or `panic!`. The collate, sort and deduplicate errors name the input directory. The dedup arm used to drop the reason.
  - libradicl's message is kept as the cause, so a too-new file still says "RAD spec major version 3 is newer than supported (2); please update this tool".
- **`view`.**
  - A multi-barcode (Flex) or scATAC RAD now gets "`alevin-fry view` supports only single-barcode scRNA-seq RAD files, but <path> is a …" instead of the `b`/`u` name asserts.
  - `convert::view` now returns `anyhow::Result<()>` and `main` uses `?` (previously it called `view2(..).unwrap()`).
  - The b/u name loop is removed. The role-preferring record context already validates those tags.
- **USA mode** (3-column tg-map):
  - `--num-bootstraps` is now an `ensure!`; it used to be an `assert_eq!`.
  - `-r trivial` is now refused up front. It used to panic with index out of bounds after writing partial output.
  - Both checks run before the output directory is created.
- **Multi-sample knee mode.** `get_knee` needs at least 3 distinct barcodes.
  - In knee mode, `compile_multi_sample_cell_output` now skips samples with 1–2 barcodes, the same way it skips empty samples: WARN, `num_cells` 0, `num_reads` 0, no permit files.
  - Other filter methods are unchanged, and `get_knee` itself is unchanged.
  - Single-sample knee mode on 1–2 barcodes still fails, as chosen in 2f09327, but with an error naming the alternatives instead of the assert.
  - `docs/source/generate_permit_list.rst` now says this in one sentence under `--knee-distance`.
- **scATAC permit list that keeps 0 barcodes.** `process_unfiltered` writes its outputs as before, including `generate_permit_list.json` with `correction_stats`, then returns an error.
  - It counts unmatched reads whose reverse complement is in the permit list, using data already in memory and only on this path.
  - The error names the other orientation as the fix only when that orientation clearly fits: it must match more reads than the given one, and at least half of all mapped reads. For example: `… 0 of the 231609 mapped reads have a barcode in the permit list with --permit-bc-ori rc, but 208254 (89.92%) have one with --permit-bc-ori fw … re-run generate-permit-list with --permit-bc-ori fw (with simpleaf atac process, pass --permit-barcode-ori fw)`.
  - Otherwise the error reports both counts and `--min-reads`, and asks the user to check the permit list and the orientation, without suggesting a re-run. This is the usual case for a permit list of the wrong chemistry, which matches a few reads either way by chance: `… 5 of the 1477997 mapped reads have a barcode in the permit list with --permit-bc-ori rc (673 with --permit-bc-ori fw), and no barcode has at least --min-reads 10 reads. Check that the permit list matches the chemistry, and the barcode orientation (…)`.
  - The shared `likely_valid_permit_list` diagnostic is unchanged, and no orientation is ever chosen automatically.
- **Tests:**
  - new `tests/error_paths_integration.rs` (6 tests);
  - 3 new tests in `tests/atac_integration.rs`. The zero-barcode test covers a reversed list (hint), an unrelated list, and a list where only 25% of reads match the other way (no hint).
  - 7 of the 9 run against develop, and all 7 fail there. The 2 `view` tests cannot compile against develop, because its `view` returns `()`.

## Behavior / compatibility

- **Successful runs are unchanged.** The evidence is under Testing.
- **Failing runs exit 1 instead of 134**, with an error that names the file, directory or flag.
- **Intended changes:**
  - `generate-permit-list -k --sample-bc-list` now completes when some samples have 1–2 cell barcodes, which happens on real Flex data. Before, it aborted. simpleaf multiplex-quant passes `--unfiltered-pl`, so it is not affected.
  - `atac generate-permit-list` that keeps no barcode now exits 1. Before, it exited 0 and `atac sort` then wrote a 0-byte `map.bed`. This means `simpleaf atac process` with the wrong barcode orientation (e.g. `-c 10x-v1` on PBMC 5k NextGEM ATAC) now stops at the permit-list step, with the orientation hint in the error simpleaf prints. Before, it exited 0 with an empty BED.
  - `view` now reads role-annotated single-barcode files whose tags are not named `b`/`u`. Before, it panicked on them.
  - A non-integer `b`/`u` tag in `view` now exits 1 instead of 65.
  - The public `alevin_fry::convert::view` now returns `anyhow::Result<()>`.

## Testing

Commands and results:

- `cargo fmt --check`: clean.
- `cargo clippy --all-targets`: 0 warnings (also 0 on develop).
- `cargo test`: 117 passed, 3 ignored. On develop it is 108 passed, 3 ignored; the difference is the 9 new tests.

The new tests were also run against develop, leaving out the 2 `view` tests, which need the new signature. All 7 that ran fail there, by panicking.

**Unchanged output** (develop edfd1aa vs this branch, release builds, `-t 16`; matrices joined by cell and feature name):

| Data / mode | Result |
|---|---|
| PBMC 1k v3 USA (splici, 3-col t2g, unfiltered PL) | `permit_freq`/`permit_map` identical in content; `cr-like` and `cr-like-em` matrices identical (0 differing of 5.57M / 6.27M nnz); featureDump identical* |
| PBMC, 2-col t2g, `-r trivial` and `cr-like-em -b 2` | matrices identical |
| PBMC knee (`-k`) | `permit_freq`/`permit_map`/`all_freq` identical in content (1,152 cells) |
| Real 10x Flex 20M subsample, 384-sample list, unfiltered | matrix (204,294 cells, 14.4M nnz) and featureDump identical |
| Same, `-k` | develop aborts (134). This branch completes and is identical to develop run on the 25 samples with ≥3 barcodes: matrix (190,031 cells), and all 25 per-sample `permit_freq` and `sample_info.json` entries. The other 359 samples have `num_cells` 0 and no permit files. |
| scATAC chr21 subsample, `--permit-bc-ori fw` | `map.bed` byte-identical (36,995 lines); permit lists and `unmapped_bc_count_collated` identical in content; `bin_recs`/`bin_lens`/`correction_plan` byte-identical |
| `view` (RAD v2 single-barcode, ± `--header`; RAD v1 PBMC, first 2M lines) | stdout byte-identical |

\* In `cr-like-em`, one cell's DeduplicatedReads flips in the last float digit (45.99037 vs 45.990376). develop alternates between the same two values across 4 reruns, so this is existing run-to-run nondeterminism.

The PBMC USA, Flex unfiltered and chr21 rows were re-run with the final head.

**Error paths** (develop → this branch):

| Case | develop | this branch |
|---|---|---|
| gpl on a spec-major-3 / truncated / empty `map.rad` | 134 | 1 |
| atac gpl on a v3 / empty `map.rad` | 134 | 1 |
| collate on a v3 `map.rad` | 134 | 1 |
| collate on a zero-cell multi-sample permit list | 134 | 1 |
| atac deduplicate on a v3 collated file | 134 | 1 |
| view on a v3 / Flex / ATAC file | 134 | 1 |
| quant USA `-r trivial` | 134, partial output | 1, no output |
| quant USA `cr-like-em -b 4` | 134 | 1 |
| atac gpl `-d rc` on forward-matching reads | 0 + empty BED | 1 + hint |

**Which zero-barcode errors give the orientation hint** (`atac generate-permit-list -m 10`, real data):

| Map / permit list / `-d` | Reads matching the other orientation | Error |
|---|---|---|
| chr21 subsample, 737K-cratac-v1, `rc` (wrong orientation) | 208,254 (89.92%) | hint: re-run with `fw` |
| PBMC 5k ATAC, 737K-cratac-v1, `rc` (wrong orientation) | 1,397,046 (94.52%) | hint: re-run with `fw` |
| PBMC 5k ATAC, 737K Flex list, `rc` (wrong list) | 673 (0.05%) | generic, both counts, no re-run |
| PBMC 5k ATAC, 3M-v3 RNA list, `rc` (wrong list) | 211,096 (14.28%) | generic, both counts, no re-run |

## Merge notes

- **Suggested order** for this release: #203 (`fix/flex-sample-names`), #202 (`feat/200-umi-read-counts`), `fix/lenient-version-parsing`, `chore/rad-v2-release-hygiene`, this PR, and last #204 (`feat/probe-sum`) updated with `fix/204-explicit-flex-data-type`.
- **Heads checked on 2026-10-22:** develop edfd1aa, #202 8011bd5, #203 64c24d9, #204 d01f955, this branch c89b4e4. None of them has moved since the previous check.
- **Clean merges.** This PR merges cleanly onto develop. It also merges cleanly with #202, #203, #204, each sibling branch and `test/rad-v2-integration` (1b3de59). The new tests are in a new file (`tests/error_paths_integration.rs`) and in `tests/atac_integration.rs`; neither is touched by #203 or #204, which edit `multi_barcode_integration.rs`.
- **Full merge.** I ran the whole merge in the order above:
  - fmt is clean;
  - clippy has 0 warnings, with and without `--all-features`;
  - `cargo test`: 142 passed, 0 failed, 3 ignored.
  - Only the #204 step has conflicts, and they are between #202 and #204 (see `fix/204-explicit-flex-data-type`), not with this PR.
- **Flex and USA checks.** The USA checks sit after the tg-map summary, so they run after #204's Flex checks. A run declared Flex (`--data-type flex`) with a 3-column tg-map still gets #204's "Pass a 2-column (target, gene) tg-map" error. A multi-barcode run without the declaration is quantified per gene and gets this PR's USA errors for `-b` and `-r trivial`.
- **Docs.** The docs sentence is at line 29 of `generate_permit_list.rst`. #203 edits around line 58 and #204 around lines 62 and 77–90, and the file merges cleanly.
- **Not in this PR:**
  - 1b3de59 on `test/rad-v2-integration` makes `--dump-molecules` work on Flex probe-level data. It belongs with whichever of #202 and #204 merges second (#204 in this order).
  - simpleaf's `feat/multiplex-quant-new-alevin-fry-options` passes `generate-permit-list --data-type flex`. It must ship with or after the alevin-fry release that contains #204 and `fix/204-explicit-flex-data-type`.
  - The CHANGELOG is not edited here. A one-line note in `quant.rst` that `--num-bootstraps` is rejected in USA mode would overlap the #202 and #204 hunks there (lines 29–37). That note is left for the release PR and should go on its checklist.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01TtmwfkBMvwsCxdQrf4RTPN

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edfd1aae5426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.