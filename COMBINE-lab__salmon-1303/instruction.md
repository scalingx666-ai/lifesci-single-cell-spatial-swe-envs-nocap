# Issue

**Title:** fix(core): use one list of compressed-file suffixes

## Description

## Problem

Two lists say which suffixes mean "compressed", and they disagree:

| | `.gz` `.bgz` `.bz2` `.xz` `.zst` | `.zstd` | `.lzma` | `.bgzf` |
|---|---|---|---|---|
| `compress::strip_compression_extension` (SAM or BAM?) | yes | yes | yes | **no** |
| `genemap::COMPRESSION_SUFFIXES` (GTF or TSV?) | yes | **no** | **no** | yes |

Every format decodes fine from content, so the file opens either way. It is the question about what is underneath that goes wrong:

- `genes.gtf.zstd` or `genes.gtf.lzma` passed to `-g` was taken for a TSV. The comment on that function already says what happens then: a GTF in the TSV branch "parses into `{sequence name: source}` pairs, which is a non-empty map that matches no transcript, so it fails silently rather than loudly".
- `aln.sam.bgzf` passed to `-a` was sent to the BAM reader.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "Compressed-file suffix lists disagree." Tracked in #1283.

## Fix

One list. `strip_compression_extension` gains `.bgzf`, so it covers both, and `has_gtf_extension` calls it instead of keeping its own, which removes `COMPRESSION_SUFFIXES`.

## Behaviour change

Those three names are now read as what they are. No other name changes.

## Verification

- The new test `a_gtf_is_recognised_under_every_suffix_the_reader_can_decode` failed before the fix on `a.gtf.zstd`, and `strips_one_compression_extension` failed on the added `a.sam.bgzf` case. Both pass now.
- Tests of `salmon-core` and `salmon-align` pass, and clippy is clean. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.