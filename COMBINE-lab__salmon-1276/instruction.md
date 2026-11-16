# Issue

**Title:** fix(cli): keep decoys out of gene-level output

## Description

## Problem

With a decoy-aware index and `-g`, decoys leaked into the gene-level output. `quant.sf` hides them through `quant_row_indices`, but `write_gene_level` aggregated every reference. On this branch's base (`develop`), with the `sample_data` transcripts plus a 5 kb `chr1` decoy and a complete gene map:

```
quant.sf         0 chr1 rows
quant.genes.sf   1 chr1 row
genemap_unmatched_txps.json   {"unmatched_transcripts": ["chr1"]}
warning: 1 of 16 transcript(s) had no entry in the gene map ...
```

There are 15 transcripts, not 16, and the map covers all of them. The warning then points the user at an annotation problem that doesn't exist.

The gene map match rate is computed over the same names. A fragmented genome decoy with at least as many scaffolds as transcripts could therefore push the rate to 50% or below and trigger the false "treat this output as transcript-level" warning. That consequence comes from reading the code; it was not run on a real genome decoy.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit compared how the output writers pick their rows and saw that the gene path was the only one not using `quant_row_indices`, then confirmed it with a decoy index and `-g`. The output above was reproduced again on `develop` for this PR. Tracked in #1283 (finding 8).

## Fix

`write_gene_level` takes the rows to report, the same ones `quant.sf` uses. All six call sites pass them. The alignment-side row selection moved from `write_outputs` into `AlignQuantResult::quant_rows()`, so the two outputs share one rule.

## Verification

On the same input, after the fix: no `chr1` row in `quant.genes.sf`, no unmatched-transcript file and no warning. `quant.sf` is unchanged (`cmp` on sorted rows), and the other rows of `quant.genes.sf` are unchanged (empty `diff`).

`decoys_are_excluded_and_mass_is_conserved_with_bias` now also runs `-g` on the default path and under `--online`, and checks the gene names, the unmatched list and the warning. The CLI `decoy_bias`, `readiness_blockers` and `flag_matrix` tests, the `salmon-align` `output_contract` test, and clippy on `salmon-cli` and `salmon-align` pass. The whole workspace suite was not run on this branch; CI covers it.

Runs through `-a` and `--rad` share `quant_rows()` but have no test of their own for this.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.