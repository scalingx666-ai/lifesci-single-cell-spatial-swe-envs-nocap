# Issue

**Title:** fix(single): correct perturbation backend outputs and error handling

## Description

## Summary

- compute scTenifoldKnk KD/OE cell effects from the full WT network, independently of graph display thresholds, while preserving the native KO calculation
- scale only outgoing target rows once, avoiding changes to incoming edges and repeated scaling between multiple or duplicate targets
- read CellOracle base GRNs from AnnData without evaluating DataFrame truth values
- propagate CellOracle imputation errors instead of silently substituting raw expression
- add regression coverage and document the KD/OE approximation

## Method semantics

For scTenifoldKnk, KD/OE uses a one-step linear approximation: scale target rows of the full WT network by 1/fold_change or fold_change, then compute delta_X = X @ (W_perturbed - W_WT). This is not a native scTenifoldKnk KD/OE simulation. GRN outputs remain thresholded summaries, and their edge-based delta_expr is not predicted expression. No Dynamo support is added.

## Validation

- 32 tests passed via normal package imports: tests/single/test_perturb.py and tests/pl/test_perturbation.py
- regression coverage includes weak-edge threshold independence, signed weights, incoming-edge preservation, multiple/duplicate targets, identity perturbation, gene ordering and expression-layer selection
- real scTenifoldPy 0.4.0 run on a fixed-seed Paul2015 subset (160 cells, 64 genes; three PCNets and rank-three tensor decomposition): KO matched direct backend output; KD/OE matched an independent linear calculation within 4.5e-16; identity and repeated-target checks passed
- real CellOracle 0.20.0 run on 300 Paul2015 cells and 1,999 genes with the tutorial ATAC base GRN: KO/KD/OE delta_X matched direct Oracle simulation exactly, and an invalid imputation neighbor count propagated the original error
- real-backend runs used the public API without backend stubs or module-loading bypasses
- isolated local environment dependency check and git diff --check passed

These are numerical integration checks on real-data subsets, not biological validation of KD/OE or full-dataset benchmarks. No project dependency changes or local test artifacts are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c678ecea2ce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.