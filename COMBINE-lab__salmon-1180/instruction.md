# Issue

**Title:** fix(map): right-orphan records reported AS:i:0 instead of the anchor score

## Description

Independent fix for the one thing @BenjaminDEMAILLE flagged in #1141 as being in our category rather than his. Confirmed his report in full and fixed it as its own small PR, separate from the #1141 mapping-output decision (which stays deferred per @rob-p).

## The bug

The SAM writer reconstructs read2's `AS` as `score - r1_score`. For an orphan only one mate is placed, so the unmapped mate must contribute 0 — but both orphan constructors set `r1_score = anchor_score` unconditionally. For a **right** orphan (read1 is the unmapped mate), `score - r1_score` collapses to **0**. Left orphans were correct because the writer reads their `r1_score` directly, which is why the defect was one-sided.

## Confirmed, not assumed — 2M real fragments, selective alignment

| record class | count | before | after |
|---|---|---|---|
| left-orphan | 834,288 | ✓ real score | ✓ real score |
| **right-orphan** | **717,526** | **100% `AS:i:0`** | **100% real (min 196, max 300)** |
| paired READ1 | 22,265,435 | ✓ | ✓ |
| paired READ2 | 22,265,435 | ✓ | ✓ |

Two constructors carried it (`orphan_raw`, and the true-orphan arm of `push_orphan_or_recovered`); the proper-pair and single-end paths were already correct.

## Safety

`r1_score` feeds **only** the SAM `AS` reconstruction — it never reaches the RAD or inference (verified: no consumer outside the mapper and `mapping_record.rs`). The same `--writeMappings` run produces a **byte-identical `quant.sf`** before and after (`b6ce28f8…` both). Zero effect on quantification or determinism, exactly as Ben noted.

## The fix

One rule, `orphan_read1_score(anchor_is_left, anchor_score)`, routed through by both constructors so they cannot diverge again — which is how the right side stayed broken while the left was fixed. Unit test pins both directions and the `score - r1_score` reconstruction.

## Scope

Selective alignment only. **Sketch mode** reports `AS:i:0` for right orphans *and* for every proper-pair mate (46.5M of them), because pseudoalignment has no per-base alignment score. Giving sketch a meaningful `AS` — or omitting it — is a separate semantic question worth its own issue, deliberately not bundled here.

## Recommendation for 2.6.0

Take it. It is the same class as the output-contract fixes already merged, it is surgical and provably quant-neutral, and 2.6.0 is the release newly emphasizing output correctness — a `--writeMappings` file where 1.5% of records claim a false zero score is a poor look for it. The rest of #1141 (CIGAR synthesis, `AS`-vs-`NM` self-consistency) genuinely needs design work and stays deferred.

Validation: `cargo fmt`, `cargo clippy -p salmon-map --all-targets -D warnings`, `cargo test -p salmon-map -p salmon-quant` (110 pass, 0 fail) all clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f605741b5305`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.