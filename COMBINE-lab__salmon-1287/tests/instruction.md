# Issue

**Title:** fix(quantmerge): refuse ambiguous sample names, short rows and repeated targets

## Description

## Problem

`salmon quantmerge` produced a matrix that looked fine from input it could not represent.

- **Identical sample names:** `--quants a/quant b/quant` names both columns `quant`, because the default name is the directory's last component. The samples cannot be told apart.
- **Empty sample name:** `--quants .` gives a column with no name.
- **Truncated rows:** a row too short for the merged column was skipped, so that sample's cell became `NA`. `NA` means "target not in this sample", so damaged input looked like missing data.
- **Repeated targets:** when a target appeared twice in one file, the later row silently overwrote the earlier one.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit ran the two sample-name cases and found the truncated-row and overwrite cases by reading `merge_quants`. Tracked in #1283 (finding 16).

## Fix

All in `merge_quants` (`crates/salmon-core/src/quantmerge.rs`). Each case is now an error, and the output file is not created:

- An empty or repeated sample name. The message points to `--names`.
- A row with fewer than the 5 `quant.sf` columns, with the file and line named. This applies even when the merged column itself is present, since the row is still damaged.
- A target appearing twice in one file, with the file and line named.

Targets genuinely absent from a sample still get the `--missing` value, as before. Blank lines are still skipped.

## Behaviour change

Merges that used to succeed with these inputs now fail. Anyone with sample directories that share a last component must now pass `--names`.

## Limits

A file cut off exactly at a row boundary has only complete rows, so it cannot be detected here and still shows `NA` for the lost targets.

## Verification

- New unit tests in `quantmerge.rs`: `duplicate_or_empty_sample_names_are_refused`, `a_short_row_is_refused_and_named` and `a_target_repeated_in_one_sample_is_refused`. I saw all three fail without the fix.
- These tests call `merge_quants` directly. No test runs the `quantmerge` command end to end.
- `salmon-core` and `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.