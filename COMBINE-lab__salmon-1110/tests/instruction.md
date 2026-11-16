# Issue

**Title:** fix(align): fail on an unusable -t FASTA instead of quantifying without it

## Description

, which is merged — this is based on top of it, as agreed, so the two do not overlap. Both items here were noticed during that review and deliberately kept out of it.

## An empty or non-FASTA `-t` succeeded

`load_ref_bytes` is only reached when the error or bias models need the sequences *and* the user supplied `-t`, so a file with no records in it is a mistake, not a choice.

Unchecked, it was silent in the worst way: every reference resolved to an empty sequence, the models contributed nothing, and the run **exited 0** with numbers that were not what the user asked for. A wrong answer that looks like a right one.

```
Error: alignment-based quantification failed

Caused by:
    no sequences found in /path/to/empty.fa: expected FASTA records beginning with '>'.
    The error and sequence-bias models are built from this file, so an empty or
    non-FASTA one would silently disable them rather than fail.
```

## Read failures lost the path

The path was attached when *opening*, but decompression fails while *reading*, so a truncated `.fa.gz` reported a bare `unexpected end of file` — with nothing to say which of a run's several inputs it meant.

| | before | after |
| --- | --- | --- |
| truncated `.fa.gz` | `unexpected end of file` | `0: reading /path/to/trunc.fa.gz`<br>`1: unexpected end of file` |

## Plus: a warning when the FASTA matches nothing

Not an error — a transcriptome legitimately need not cover every reference in the alignment header, and partial coverage stays accepted (there is a test pinning that). But *no* overlap means the wrong file, and it presents identically to working correctly: models that quietly do nothing.

> none of the 15 reference(s) in the alignment input were found in `wrong.fa`. The error and sequence-bias models will contribute nothing. This usually means the FASTA does not match the alignments — check that it is the transcriptome they were aligned against, and that identifiers match (versioned vs unversioned, or a GENCODE-style `|` header).

The message names the usual causes because that is nearly always what it turns out to be — the same identifier-matching trap behind #1075 and the `--ignoreTxVersion` flag.

## Verification

| case | result |
| --- | --- |
| empty file | exits 1, names the file and what was expected |
| valid file, no FASTA records | same |
| truncated `.fa.gz` | exits 1, error names the file |
| valid FASTA, zero name overlap | exits 0 with the warning |
| **valid input** | **byte-identical `quant.sf`, no warnings** |

Four tests: the empty and non-FASTA cases, a mid-stream read failure naming the file, and partial coverage still being accepted. The first two are negative-controlled — reverting either change makes them fail, so they pin the behaviour rather than passing vacuously.

`cargo fmt`, `clippy --workspace --all-targets -D warnings` and the full suite are clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YKxqH6k1sbmDC1bpNso3zr

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9577c8e51961`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.