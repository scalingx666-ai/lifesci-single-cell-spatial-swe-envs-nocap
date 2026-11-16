# Issue

**Title:** fix(align): count unmapped BAM records in the mapping rate

## Description

## Problem

With `-a`, `percent_mapped` left out every read the aligner could not place. The BAM reader threw away unmapped records before grouping them into fragments, so they never reached `num_processed`. Bowtie2 keeps unmapped reads in its output by default, and so does STAR with `--outSAMunmapped Within`, so a poor library looked perfect:

| 2000 mapped pairs + 6000 unmapped pairs | `num_processed` | `num_mapped` | `percent_mapped` | `low_mapping_rate` diagnostic |
| --- | --- | --- | --- | --- |
| before, default and `--online` | 2000 | 2000 | 100.0 | no |
| after, default and `--online` | 8000 | 2000 | 25.0 | yes |

The docs already define `num_processed` as "fragments observed, mapped or not", and that is what it means in reads mode. Only the BAM paths disagreed.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit read the three BAM reader loops and saw the same `is_unmapped` skip ahead of the counting, then confirmed it with a generated SAM. The table above was measured on `develop` for this PR, with a SAM of the same shape. Tracked in #1283 (finding 10).

## Fix

The skip is removed from all three reader loops: `bam_rad.rs`, `genome_project.rs` and the online path in `lib.rs`. No new filter is needed. `record_to_frag` and `record_to_genomic_alignment` already drop unmapped records, so a wholly unmapped fragment now counts as processed and ends there, and a half-mapped pair keeps only its mapped record, as before.

- `process_fragment` returns early on an empty fragment, so it reaches no strand or format tallies.
- The log wording no longer says "aligned fragments" for a count that now includes unaligned ones.

## What does not change

Only the counts change. `quant.sf` is byte-identical before and after on the input above, on both the default path and `--online`.

The cost is that unmapped records now travel through the reader's grouping and batching, so an unmapped-heavy BAM uses a little more reader work and memory. I did not measure it.

## Verification

New test: `unmapped_fragments_count_against_the_mapping_rate`, which covers `--online`, `write_alignment_rad` and `quantify_rad`. All `salmon-align` and `salmon-cli` tests and clippy on both crates pass. The whole workspace suite was not run on this branch; CI covers it.

`genome_project.rs` gets the same one-line removal, but it has no test or run with unmapped records in this PR: it relies on the existing `record_to_genomic_alignment` check and `gas.is_empty()` guard, which I read but did not exercise.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.