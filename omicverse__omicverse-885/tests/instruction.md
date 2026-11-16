# Issue

**Title:** refactor: drop inmoose from milo & pyDEG edgepy (pure-Python pyedger)

## Description

## Summary
Removes the **last two uses of `inmoose`** in omicverse, routing both through the vendored pure-Python `pyedger` (edgeR) port. `import omicverse` and DEG/DA no longer touch inmoose or R.

- **`ov.single.Milo.da_nhoods`** — NB-GLM now runs `DGEList → estimateDisp(trend='none') → glmQLFit(robust=False, legacy=False) → glmQLFTest`, the same engine `miloR::testNhoods` wraps. `legacy=False` = edgeR 4.x / miloR default bias-adjusted QL.
- **`ov.bulk.pyDEG.deg_analysis(method='edgepy')`** — edgeR classic GLM likelihood-ratio test via `pyedger` `glmFit`+`glmLRT` (now reports the GLM's own log2FC instead of the old pseudo-count mean ratio). No inmoose / R.

## R-parity validation (CMAP: Bioconductor edgeR 4.4.0 + miloR)
Synthetic 150-nhood × 8-sample count matrix, identical pipeline on both sides:

| metric | pyedger vs edgeR (same cfg) | pyedger vs miloR-engine (trended + robust=TRUE) |
|---|---|---|
| **logFC** | **bit-exact** (Pearson 1.0, max\|Δ\| 1.6e-4) | bit-exact (max\|Δ\| 5.4e-5) |
| F | Pearson 0.9958 | Pearson 0.9961 |
| PValue | Spearman **0.9966**, top-20 19/20 | Spearman 0.9968, top-20 19/20 |

**logFC is bit-exact vs Bioconductor edgeR.** F / PValue are very-high agreement but **not** bit-exact: pyedger's quasi-likelihood variance moderation (`squeezeVar`) is not yet a bit-exact port of limma's. This is a pre-existing pyedger characteristic (also affects `method='edger'`), *not* a regression — the old inmoose path was itself `robust=False` and used the older `estimateGLMCommonDisp`. Closing the F/PValue gap = a follow-up limma-`squeezeVar` port in pyedger.

## Tests
- `tests/single/test_milo_pyedger_parity.py` — pins logFC vs a committed edgeR reference + asserts F Pearson / PValue Spearman > 0.99, and runs `da_nhoods` end-to-end with `inmoose` import blocked.
- `method='edgepy'` added to `tests/bulk/test_deg_backends.py` parametrization.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4d6e627f92a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.