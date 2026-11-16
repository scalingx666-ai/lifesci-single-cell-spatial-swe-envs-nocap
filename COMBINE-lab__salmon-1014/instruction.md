# Issue

**Title:** feat(quant): abundance-aware fragment-length-distribution training

## Description

## Summary
Train the fragment-length distribution with **abundance-aware** stochastic acceptance, the last step to match C++ salmon's FLD on multimapping-heavy data. Builds on #1013.

The online abundance estimate now runs unconditionally (previously only when bias correction was on) and its per-fragment posterior is used to accept FLD samples — mirroring salmon's `if (r < exp(aln.logProb)) fragLengthDist.addVal(...)`, where `aln.logProb` includes `transcriptLogCount`. For reads shared between near-duplicates this preferentially samples the dominant transcript's implied length, concentrating the FLD (the deterministic confidence-weighting in #1013 narrowed but didn't fully match it). The offline EM does not read the online estimate, so enabling it always only affects bias collection (unchanged when off) and FLD training.

## Why this is the default (not a flag)
Investigated whether the always-on online estimate costs throughput; it does **not**:
- 3-rep matched-load 36M timings: abundance-aware **98.9s** vs prior **101.3s** (−2.4%, within noise).
- Subsampling the online update to 1/33 changed neither wall time nor accuracy → the per-fragment online work is not a bottleneck, so no subsampling/gating knob is needed.
- Determinism is *better*: run-to-run Spearman spread 0.00006 (vs 0.00043) — the FLD aggregate is stable enough that the per-thread RNG adds no meaningful nondeterminism.

## Validation vs C++ salmon 1.12.0
Polyester ground truth (human, 193,760 txps), per-transcript Spearman gap to C++:

| | #1013 (FLD-term) | this PR (abundance-aware) |
|---|--:|--:|
| easy / VBEM | 0.0025 | **0.0019** |
| easy / useEM | — | **0.0012** |
| hard / VBEM | 0.0022 | **0.0002** |
| hard / useEM | — | **0.0004** |

Real-data 36M GEUVADIS C++ parity: NumReads Pearson 0.99955, **Spearman 0.97096** (was 0.97052); mapping rate identical (92.18%). fmt + clippy clean; tests pass.

The residual gaps are now at/near the run-to-run noise floor across both difficulty levels and both EM modes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6d5d06275221`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.