# Issue

**Title:** fix(map): penalize indels hidden between read-overlapping MEMs

## Description

## Summary

`anchored_align_score` (the default PuffAligner-style scorer) treated any two adjacent chain MEMs that overlap in the read as a *pure overlap* (`score -= max_overlap * match`). Because raw k-mer anchors always overlap in the read, a small **reference-side indel** between two otherwise-exact blocks — i.e. when the two MEMs sit on different diagonals (`read_overlap != ref_overlap`) — was silently absorbed, with **no gap penalty and no DP**. That inflated the alignment score and kept transcripts the read does not actually match well.

### Concrete case
`ERR188044.600028` vs `ENST00000677249.1` carries a 3 bp insertion relative to the transcript. Two MEMs overlapped by **1 base in the read but 4 in the reference** (a 3 bp diagonal jump). The old branch scored it **152** (perfect); the true optimum is **134**. The inflated score cleared the `minAlnProb` keep filter, so Rust retained the transcript, while C++ (PuffAligner gap DP) **and Rust's own `--fullLengthAlignment` path** both score 134 and correctly drop it.

## Fix
Unify the gap/overlap handling: compute the per-axis overlap, trim both MEM ends back to a common boundary, then DP-align the residual.

* **same diagonal** → residual empty → gap DP returns 0 (old behavior preserved)
* **gap-separated** → DP the gap (old `if` branch preserved)
* **shifted diagonals** → residual exposes the indel, charged an affine gap

This matches the full-length DP and PuffAligner. Note: uni-MEM extension would **not** fix this — the indel-at-MEM-boundary geometry survives extension; it's a scoring issue, not a seeding one.

## Validation
1M-read GEUVADIS subset (ERR188044), matched dedup indices, C++ run with `--orphanChainSubThresh 0.0` to match Rust:

| metric | before | after |
|---|---|---|
| C++/Rust identical target set | 97.53% | **99.14%** |
| mean per-read Jaccard | — | 0.99628 |

Adds a deterministic regression test (`overlapping_mems_on_shifted_diagonals_incur_gap_penalty`) exercising the exact `read_ov=1, ref_ov=4` geometry (asserts score 134, not the inflated 146).

## Notes
Remaining C++/Rust divergence (0.86%) is under investigation (Rust is the strict superset on ~6k reads); fixes for that may be added to this PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Update: scope is broader than hidden indels
This same unified gap/overlap fix also resolves an over-scoring case where two exact MEMs **overlap in the read but are separated by a reference gap** (different diagonals) — a partial-paralog placement (one mate shares a block with a paralog but diverges elsewhere). The old branch absorbed the reference gap as a plain overlap and credited a perfect score, so Rust reported partial-paralog targets that C++ and the true full-length DP reject. With this fix, on the human easy-sim (matched keep-dup indices): C++/Rust target-set concordance **99.227% → 99.908%** (and *balanced* — closer to C++ than even full-length DP), and accuracy-vs-truth Spearman(expr) **0.86765 → 0.86912** (≈ full-length 0.86914 ≈ C++ 0.86963), without the full-length DP cost. (The uni-MEM-default PR #1018 carries a byte-identical copy of this hunk so it's correct standalone; it will merge cleanly with this PR.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9604e2114029`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.