# Issue

**Title:** fix(align): warn when a -t FASTA sequence has another length than its reference

## Description

## Problem

`-t` FASTA sequences are matched to the input's references by name only. If a sequence has the right name but a different length (another release or assembly of the transcriptome), nothing says so. The error and bias models then read whatever bases sit at those positions, or nothing past the end, and the run reports success.

The loader already warns when *no* name matches, because that "presents as models that do nothing rather than as a mistake". A wrong-version FASTA has the same effect and got no warning. For example, an `@SQ ... LN:1000` matched with a 700 bp `>t` was accepted in silence.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "`-t` FASTA is matched to `@SQ` by name only, so wrong lengths go unnoticed." Tracked in #1283.

## Fix

`load_ref_bytes` now takes the input's reference lengths and warns with the number of mismatches and the first example. All three callers pass them: the `-a` online path, `-a` deterministic (`bam_rad`) and `--rad`.

Two cases do not count:
- **An absent reference:** a FASTA need not cover every reference, as the loader already says.
- **A FASTA sequence longer only by a run of `A`:** `salmon index` clips poly-A tails, so a RAD's lengths legitimately lack them and the raw FASTA would otherwise warn on ordinary runs. Positions still line up in this case.

## Behaviour change

A warning only. I chose not to refuse the run: an aligner's reference may have been edited in ways that are harmless to the user, and it was accepted until now.

## Limits

- The check compares lengths only. A same-length different sequence still goes unnoticed.
- A reference clipped by something other than a poly-A tail still warns, by design.

## Verification

- New unit test `a_wrong_length_is_a_mismatch_but_absent_or_a_clipped_tail_is_not`.
- By hand, on a SAM with `LN:1000` under `-a`, with and without `--seqBias`: the same-length FASTA and the one with a 30 bp poly-A tail print nothing, and the 700 bp one warns.
- Tests of `salmon-align` pass, and clippy is clean. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.