# Issue

**Title:** fix: reject stale multi-sample collations; apply --sample-names

## Description

Follow-up to an issue noticed while validating #202 on a Flex dataset.

## Problem

Quant reads each multi-sample record's sample index from `barcodes[0]` and looks it up in the names from `collation_manifest.bin`. Collations written before 0.15.0 stored the sparse *plate position* there rather than the manifest ordinal. That was fixed for new collations in 17986c0 (simpleaf#195), but quant still accepted old collations silently:
- an **out-of-range** index dropped the `sample_name` field, so those `featureDump.txt` rows had 9 fields under a 10-column header;
- an **in-range** index attached the **wrong** sample name.

Separately, `generate-permit-list --sample-names` was parsed and stored but never used. Sample names came only from the 3-column `--sample-bc-list` format.

## Changes

- **quant:** refuses a multi-sample collation whose `collate.json` `version_str` is below 0.15.0, asking for it to be re-collated. A collation without a readable version is still accepted.
- **quant:** a sample index outside the manifest is now an error (the run fails, and no `quant.json` is written), instead of producing a malformed row.
- **generate-permit-list `--sample-names`:** applies its `barcode<TAB>name` file. Any barcode of a sample (a rotation or the canonical barcode) may name it; barcodes of one sample must agree; names must be distinct; unknown barcodes, wrong lengths and malformed lines are rejected. Reverse-oriented whitelists are handled. The loader's packing and orientation code moved into shared helpers.
- **Docs:** the sample-barcode list formats and `--sample-names` are documented in `generate_permit_list.rst`.
- **Tests:** the multi-barcode and role-driven integration tests passed a fake `0.12.0` version to collate; they now use the crate version.

## Validation

Human Kidney 4k GEM-X Flex (`map_output3`):

| case | result |
|---|---|
| quant on the old 0.11.2 collation | fails: "this multi-sample collation was written by alevin-fry 0.11.2, which recorded plate positions rather than sample ordinals … re-run `alevin-fry collate` with 0.15.0 or later" |
| same collation with `collate.json` version removed | fails: "cell TCCGTTAAGGCGGATC has sample index 2850, but collation_manifest.bin names only 1 samples …" |
| GPL + collate + quant with current code | succeeds; all 66,635 `featureDump.txt` lines have 10 fields |
| 3-column 10x list + `--sample-names` renaming all samples | 32 samples renamed (`kidney_AB001`, …); `featureDump.txt` and row names identical to the run without names, apart from the names |
| 1-column list + names mapping several barcodes to one name | rejected: "more than one sample is named 'BC001'" |

New unit tests cover version parsing, the version check, and `--sample-names` (renaming through a rotation, repeated consistent names, conflicts, duplicate names, unknown barcodes, malformed lines, wrong length, and reverse orientation). The full suite passes in debug and release; clippy and fmt are clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RRoQ4mpDcUwtsSz5aedxtM

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edfd1aae5426`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.