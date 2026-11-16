# Issue

**Title:** fix(index): refuse a decoy list that names sequences missing from the FASTA

## Description

## Problem

A decoy list that matched nothing was accepted without a word. The most likely way to get there is a list made with `grep '^>'` that was never cleaned up, so every name keeps its `>`:

```
>chr1          # decoys.txt
>chr1 dna      # FASTA header
```

The build exited 0, `info.json` recorded `first_decoy_index: null, num_decoys: 0`, and `chr1` then got its own row in `quant.sf`. The genome was being treated as a transcript: reads could be assigned to it, and its `N` bases were randomized as a transcript's are. A partial miss was just as silent.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit noticed that the "no decoys found" branch in `build()` returns `(None, 0)` with no log line, then confirmed the effect on `sample_data.tgz` with a synthetic `chr1` appended. Tracked in #1283 (finding 7).

## Fix

`preprocess_fasta` now tracks which listed names it met, and fails with the number of unmatched names and the first five, sorted. The check runs before anything in the index is replaced, so a bad list costs no existing index.

## Behaviour change

A list that names sequences absent from the FASTA used to build and now fails, even when the other names matched. A deliberately oversized list, such as all the contigs of an assembly against a subset FASTA, would have to be trimmed. A strict check seemed right because a mismatch here means the list and the FASTA disagree, but a warning for the partial case would be an easy change if you prefer it.

## Verification

Same FASTA (`sample_data` transcripts plus a 5 kb `chr1`), same list:

| | Exit code | Result |
| --- | --- | --- |
| before, list holds `>chr1` | 0 | `num_decoys: 0`, one `chr1` row in `quant.sf` |
| after, list holds `>chr1` | 1 | `1 name(s) in the decoy list match no reference in the FASTA, e.g. [">chr1"]. Names must be the header up to the first space, with no leading `>`.` |
| after, list holds `chr1` | 0 | `num_decoys: 1` |

New test: `unmatched_decoy_names_are_refused`. `salmon-index` tests, clippy on `salmon-index`, and the CLI `decoy_bias`, `metadata_truth` and `output_contract` tests pass. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.