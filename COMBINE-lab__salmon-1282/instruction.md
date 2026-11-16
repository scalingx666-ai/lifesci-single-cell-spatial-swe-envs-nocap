# Issue

**Title:** fix(rad): keep each orphan's own side and drop orphans beside a proper pair

## Description

## Problem

A RAD record stores one `frag_map_type` for the whole fragment, and the reader applies it to every hit. `fragment_level` picks the "most complete" status when placements disagree, so the others are overwritten. On the default `-a` path this gives wrong counts with no warning. Two cases, both measured with the new tests:

**Left and right orphans of one fragment.** R1 alone on `txA`, R2 alone on `txB`, under `-l ISR`, 1000 fragments. Both placements are valid and the fixture is symmetric, but one placement is judged on the wrong mate's strand and filtered. Which transcript loses depends on record order.

| | `txA` | `txB` |
|---|---|---|
| before | 0 | 1000 |
| after | 500 | 500 |

**An orphan beside a proper pair.** A proper pair on `txA` and R1 alone on `txB`, 500 fragments. The orphan is read back as a pair, and its read length (in the same slot) as a fragment length. With a 300 bp orphan and 300 bp fragments, it gets the pair's full weight.

| | `txA` | `txB` |
|---|---|---|
| before | 250 | 250 |
| after | 500 | 0 |

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit read `fragment_level` and `placements_into` side by side, saw that the writer summarises per-hit statuses that the reader then needs, and reproduced the `txA=0, txB=1000` result on a small synthetic SAM. It was the audit's first must-fix finding. Tracked in #1283 (finding 1).

## Fix

- **Pair beside orphans:** the BAM and genome writers drop a fragment's orphans when it has a proper pair. `salmon-map/src/mapper.rs` already applies this rule ("A concordant pair to a transcript discards every orphan"). It happens before the FLD and naive eq-class tallies, so they see what gets written.
- **Left and right orphans:** new `SalmonBulkRecord::from_placements`, used by all three writers. A hit on the side `frag_type` does not name sets its `mate_fw` bit, which `RadHit::for_placement` otherwise forces to false on an orphan hit. The reader flips the status for those hits.

## Compatibility

No new tag and no layout change. I used the spare bit rather than the new record type the audit suggested, because a new type would make older readers misread the file.

- Records with one orphan side are byte-identical to before, so existing RADs read as they did.
- Only salmon RADs are affected. Piscem records go through their own `placements_into`.
- An older salmon reading a new RAD treats a mixed record as it does today: same wrong status, no failure.

## Behaviour change

Counts change for fragments mixing a proper pair and orphans on the default path. `--online` still keeps those orphans with its orphan penalty, so the two paths apply different rules here. I did not change `--online`.

## Verification

- New tests in `crates/salmon-align/tests/deterministic_bam.rs` for both cases, and `mixed_orphan_sides_are_marked_in_the_encoded_hit` in `crates/salmon-rad/tests/roundtrip.rs`. I saw both integration tests fail without the fix, with the "before" numbers above.
- The genome path's change has no test of its own: it shares `from_placements`, but its orphan drop is only covered by the existing suite.
- `salmon-rad`, `salmon-align`, `salmon-quant`, `salmon-map` and `salmon-cli` tests pass, and workspace clippy is clean with `-D warnings`. The whole workspace suite was not run on this branch; CI covers it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5deb220941f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.