# Issue

**Title:** fix(index): refuse a reference name that appears more than once

## Description

## Problem

The index build removes duplicates by sequence, but never checks names. Two FASTA records named `t1` with different sequences both enter the index, and `quant.sf` gets two `t1` rows (audit run). Gene maps and `quantmerge` identify a transcript by name, so they cannot tell those rows apart, and counts can later be merged or overwritten with no warning.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit saw that `preprocess_fasta` deduplicates only on a sequence digest, then built an index from a FASTA with a repeated name and read the two rows in `quant.sf`. The downstream effect on gene maps and `quantmerge` comes from reading the code. Tracked in #1283 (finding 17).

## Fix

`preprocess_fasta` keeps a set of processed names and stops with an error naming the repeat. The check runs on every record, before the sequence deduplication, so it applies with and without `--keepDuplicates`.

"Processed name" is the one the index stores: the header up to the first space or tab, and up to the first `|` under `--gencode`.

## Behaviour change

FASTA inputs that used to build now fail. Please check two cases:

- **Same name, same sequence:** this used to collapse silently without `--keepDuplicates`, which was harmless to the counts. It is now refused too, for example when one file is passed twice. Keeping it would be a small change if you prefer that.
- **`--gencode`:** the name stops at the first `|`, so any annotation whose records share that first field would now fail. I did not test this against a real GENCODE file. PAR_Y records in older releases are the case to check.

## Verification

- New unit test `a_repeated_transcript_name_is_refused` in `crates/salmon-index/src/lib.rs`, covering different sequences and identical ones, with and without `--keepDuplicates`. I saw it fail without the fix.
- `salmon-index`, `salmon-map` and `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.