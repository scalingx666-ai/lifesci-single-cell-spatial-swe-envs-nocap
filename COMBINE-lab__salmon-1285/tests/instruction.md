# Issue

**Title:** fix(align): take --hardFilter's best score over placements the filters keep

## Description

## Problem

`--hardFilter` keeps a fragment's top-scoring placements. On the RAD path, that top score was taken over all placements, before the strand and orphan filters run. If the best score belongs to a placement `-l` then drops, nothing reaches the bar and the fragment is lost whole.

Measured with `-l ISF` on 1000 fragments, each with a correct-strand pair on `txA` at `AS:i:-10` and a wrong-strand pair on `txB` at `AS:i:0`:

| `-l ISF --hardFilter` | `num_mapped` | `txA` |
|---|---|---|
| before | 0 | 0 |
| after | 1000 | 1000 |

Without the flag, all 1000 fragments were already kept. So the flag silently emptied a stranded sample in this case.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit saw `best` computed before the filter loop in `rad.rs`, then reproduced the loss by running a small synthetic SAM with and without the flag. Tracked in #1283 (finding 14).

## Fix

New `best_kept_score` in `crates/salmon-align/src/rad.rs`: the best score over placements that `--discardOrphans` and the strand filter keep. The eq-class pass and the bias pass both use it, so they keep the same placements.

A wrong-strand placement counts only when it is dropped, that is when `ignore_incompat` is on. With a non-zero `--incompatPrior` it stays in the run with a penalty, so it still counts.

## Behaviour change

`best` also feeds the soft score weight, so that basis shifts when the top placement is filtered. Every kept placement of a fragment shifts by the same amount, so their relative weights do not change.

## Limits

This covers the RAD path only, as the audit did. I did not check whether `--online` or reads mode have the same ordering problem.

## Verification

- New test `hard_filter_ignores_the_score_of_a_wrong_strand_placement` in `crates/salmon-align/tests/deterministic_bam.rs`. I saw it fail without the fix (`0` versus `1000`).
- `salmon-align` and `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.