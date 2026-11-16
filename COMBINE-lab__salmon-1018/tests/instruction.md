# Issue

**Title:** feat(map): make uni-MEM the default seeding mode

## Description

## Summary
Make **uni-MEM seeding the default** for selective-alignment quant (was sparse fixed-k k-mer anchors). Adds `--sparseSeeds` to opt back into the previous behavior; `--uniMEMs` is still accepted (now redundant). Pseudoalignment (`--sketch`) is unaffected — it's a separate path.

**Stacked on #1017** (the uni-MEM correctness + perf fixes), which this depends on.

## Validation
1M ERR188044 human + 2M yeast sim (vs an independent bowtie2 reference quant):

**Accuracy — yeast sim vs bowtie2 reference (NumReads):**
| mode | Spearman | Pearson | MARD |
|---|---|---|---|
| sparse | 0.98918 | 0.98584 | 0.0592 |
| **uni-MEM** | **0.98942** | **0.98599** | **0.0588** |
| C++ | 0.97360 | 0.97416 | 0.0863 |

uni-MEM is marginally better than sparse on every metric, and both Rust modes are closer to the independent reference than C++.

**C++ parity (NumReads Spearman):** uni-MEM is marginally closer to C++ than sparse on both datasets — human 0.94830 vs 0.94817; yeast 0.99216 vs 0.99207.

**uni-MEM vs sparse (the actual switch):** near-identical quant — human Spearman 0.996 / MARD 0.017; yeast 0.99995 / MARD 0.001. Same mapping rate (92.22% human, 100% yeast).

**Speed:** ~11% faster mapping phase (interleaved A/B), confirmed at 10M reads.

## Net
Negligible quant change, marginally more accurate and more C++-faithful, and faster. Verified end-to-end: default output is byte-identical to `--uniMEMs`, and `--sparseSeeds` is byte-identical to the prior default; the flags are mutually exclusive.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Update: human accuracy vs ground truth (polyester easy + hard sims, matched duplicates-kept indices)
Spearman (expressed) / MARD vs true counts:
| sim | sparse | uni-MEM | C++ |
|---|---|---|---|
| easy (104,758 expr) | 0.86775 / 0.4944 | 0.86765 / 0.4941 | 0.86963 / 0.4904 |
| hard (101,200 expr) | 0.84829 / 0.5615 | 0.84826 / 0.5612 | 0.84829 / 0.5614 |

uni-MEM and sparse are **statistically indistinguishable** (4th–5th-decimal, mixed direction), same mapping rate (~99.99%). Confirms the default switch is accuracy-neutral on real human ground truth (the small C++ lead on `easy` is the broader Rust↔C++ marginal-concordant gap, not seed-mode-specific).

## Update: also fixes a general chainer bug (contained anchors)
Investigating the residual superset surfaced a separate, pre-existing `chain_mems` bug: the colinear DP only required a successor to *start* after its predecessor, so an anchor fully **contained** in its predecessor (a repeat-copy on a different diagonal) was chained, and the anchored scorer then tanked a perfect full-length anchor below threshold (e.g. a 76 bp exact mate + a contained 37 bp repeat hit scored 62 instead of 152 → wrongly dropped). Fixed by rejecting a predecessor link when the successor's end doesn't advance on either axis. **General fix — helps both seed modes:**
- accuracy vs truth (easy-sim, Spearman expr): sparse 0.86775→**0.86920**, uni-MEM 0.86912→**0.86930** (both ≈ C++ 0.86963);
- C++/Rust concordance 99.908% → **99.934%** (balanced: Rust-superset 320 / C++-superset 308).

The remaining ~0.03%-each-way is genuine equally-best paralogs where the piscem vs pufferfish *index* enumerates occurrences slightly differently (symmetric, accuracy-neutral).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34c7cb9e61ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.