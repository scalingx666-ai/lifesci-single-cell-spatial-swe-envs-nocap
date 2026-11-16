# Issue

**Title:** fix(quant): include fragment-length probability in equivalence-class weights

## Description

## Summary

Include the fragment-length-distribution (FLD) probability in the selective-alignment **equivalence-class weights**, and train the FLD weighted by per-fragment confidence. This closes most of a small per-transcript quantification gap vs C++ salmon on multimapping transcripts.

## Root cause

The SA eq-class weights were built from the bare coverage weight, omitting the FLD term that salmon folds into its per-fragment auxProb:

```
// SalmonQuantify.cpp
double auxProb = logFragProb + logFragCov + logAlignCompatProb;   // <- logFragProb (FLD) was missing in the port
```

The missing FLD term flattened the conditional weights for paralogs/isoforms whose implied insert size differs, coarsening the range-factorized equivalence classes and slightly degrading how multimapping reads are split. A secondary issue: the port trained its FLD by adding every best-pair length at full weight (vs salmon's probability-weighted, burn-in-limited stochastic training), overdispersing the FLD on near-duplicate-rich inputs.

## Changes (`crates/salmon-quant/src/processor.rs`)

1. Fold `fld.pmf(fragment_len)` into the eq-class weight. Matches salmon's auxProb composition (FLD + coverage); the start-position term is intentionally **excluded** because effective length is applied separately in `update_eff_lengths` (including it would double-count). Gated on `pre_burnin` to mirror salmon's `numPreAuxModelSamples`.
2. Train the FLD weighted by each fragment's best-pair posterior confidence — a deterministic analog of salmon's stochastic training — so ambiguous multimappers no longer overdisperse it.

## Validation (vs C++ salmon 1.12.0)

**Polyester ground truth** (human, 193,760 txps; per-transcript Spearman, expressed):

| sim / mode | C++ | Rust before | Rust after | gap closed |
|---|--:|--:|--:|--:|
| easy / VBEM | 0.8696 | 0.8534 | 0.8671 | 85% |
| easy / useEM | 0.8916 | 0.8756 | 0.8904 | 93% |
| hard / VBEM | 0.8485 | 0.8292 | 0.8479 | 97% |
| hard / useEM | 0.8770 | 0.8564 | 0.8761 | 96% |

**Real-data 36M GEUVADIS C++ parity:** NumReads Pearson 0.9986 → **0.9995**, Spearman 0.9645 → **0.9706**. Bias path (`--gcBias --seqBias`) also improved (0.9958 → 0.9984 Pearson), no drift.

**No regressions:** mapping rate identical; 36M wall within noise; sample_data parity intact (0.9999); fmt + clippy clean.

## Residual (follow-up)

A small **systematic** residual remains (~0.0026 Spearman on easy/VBEM; ~18σ above run-to-run noise, so real, not arbitrary tie-breaking). Decomposition:
- It is *not* eq-class granularity (post-fix Rust is actually finer, 424k vs 410k classes).
- It is Rust leaking ~0.03–0.04% of reads onto true-zero near-duplicates. Part of it is VBEM sparsity (C++ drives true-zero near-dups to zero slightly harder; the lean shrinks under `--useEM`), and part is a small base weight/binning difference that survives under plain EM.
- **Not** `logAlignCompatProb`: both the polyester sim and the GEUVADIS data are unstranded (IU, 100% compatible), so that term is log(1)=0 in both tools and already matches. The base residual is in the coverage-weight / range-factorization-binning interaction (~0.03% of reads), tracked as a separate follow-up.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9164df2136e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.