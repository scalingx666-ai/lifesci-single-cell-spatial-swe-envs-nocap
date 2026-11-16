# Issue

**Title:** fix(group 1): refuse inputs and flag combos that produced a wrong answer

## Description

**Group 1 of 4** from the readiness sweep (#1140). Everything here produced *a wrong answer presented as a right one*: a clean `quant.sf` and exit 0 over data salmon had silently discarded, or a request it had silently dropped.

| Item | Was | Now |
|---|---|---|
| Invalid `-l` | Hard error in reads mode; **silently accepted** in `-a`, `--rad` and genome projection, quantified as unstranded (every call site discarded the parse error with `.ok()`) | Validated once before mode dispatch — same answer everywhere, message lists the accepted forms |
| `-r` with `-1/-2` | Single-end reads silently dropped; `cmd_info.json` still recorded them | clap conflict |
| `--noLengthCorrection` + `--seqBias`/`--gcBias`/`--posBias` | Bias silently discarded (`bias_on = (…) && !no_length_correction`), and `meta_info.json` still said `gc_bias_correct: true` | Errors at invocation, naming both sides |
| Truncated FASTQ | Quantified to the last complete record — 8 KB of an 84 KB file gave a normal-looking run over 38 of 400 reads | Refused |

## On the truncation check

Worth knowing what it does and doesn't do. Compressed inputs were **already correct** — a short gzip/zstd/bzip2/xz stream fails in the decompressor — so the preflight covers uncompressed files only, and skips anything with a compression magic.

It's exact rather than heuristic, on two invariants that cannot reject a valid file:
1. a valid FASTQ is a whole number of 4-line records;
2. its final record has a `+` separator and sequence/quality lines of equal length.

Both are needed. My first attempt used only the line count, and the test caught it: a byte-level cut can leave a multiple-of-4 line count whose last line is a partial quality string. The structural check also means a valid file with **no trailing newline** is still accepted — that ruled out the cheaper "must end in `\n`" test.

The line-boundary cases were inconsistent with each other before this: a trailing 1 or 2 orphaned lines were dropped in silence while 3 errored. That asymmetry is in the reader; it's recorded in #1162 as an upstream item. salmon now rejects all three regardless.

## Tests

Each case drives the binary end to end, with controls proving valid input still runs: every `-l` spelling including `A`, `--noLengthCorrection` alone, and intact plain **and gzipped** FASTQ.

Suite **324/0**, clippy clean. Groups 2–4 follow as separate PRs; Group 5 is tracked in #1162.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016cfXr9P5JDqoEtafmTGpNs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a4362a0c8e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.