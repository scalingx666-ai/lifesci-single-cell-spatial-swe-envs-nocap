# Issue

**Title:** fix(map): apply the pairing rules to a mate rescued by --recoverOrphans

## Description

## Problem

`--recoverOrphans` searches a fragment-length window for a mate that left no seeds, then calls the result a proper pair. It did not apply the rules normal pairing applies, so a pair that `join_reads_and_filter` refuses as dovetailed could be accepted once it came through recovery.

For example, with a 100 bp forward anchor at 200..300 and a 60 bp mate at 220..280, the rescue reported `PairedEndPaired` with `fragment_len: 80`, a fragment shorter than one of its own reads. The same fragment with seeds on both mates is rejected. So the answer depended on whether the mate had seeds, and the recovered length fed the fragment-length model and effective lengths.

The length limit was not checked either: the reverse-anchor branch computes the length from the read's nominal length, so an alignment with gaps could come out above `--fragLen` maximum.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. It was one of the audit's smaller findings, reported in one line: "`--recoverOrphans` accepts pairs the normal pairing rejects." Tracked in #1283.

## Fix

`is_dovetailed`'s test moves into `extents_dovetail`, which works on `(start, end)` extents because a rescued mate has no candidate. `recover_mate` applies it unless dovetails are allowed, and also applies the `0 < length <= max` check normal pairing uses. A refused rescue returns `None`, so the anchor stays an orphan, as it would without `--recoverOrphans`.

## Behaviour change

Only `--recoverOrphans` runs change. Some fragments reported as pairs become orphans, and fragment lengths shorter than a read leave the distribution.

## Limits

The rescued mate's start is still taken from its nominal read length, as the code already did for `r1_pos`/`r2_pos`. With gaps in the rescued alignment the extent can be off by the gap size, so a borderline dovetail could go either way.

## Verification

- The new test `orphan_recovery_refuses_a_dovetailed_mate` covers a forward anchor, a reverse anchor, and `allow_dovetail`. It failed before the fix with the `fragment_len: 80` pair above.
- Tests of `salmon-map` and `salmon-quant` pass, as do `readiness_blockers` and `mode_applicability` in `salmon-cli`. Clippy is clean. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.