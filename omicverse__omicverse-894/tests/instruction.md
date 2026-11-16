# Issue

**Title:** feat(single): add CAMEX as a cross-species backend (method='camex')

## Description

## Summary

Adds **CAMEX** (Guo et al., *Nat. Commun.* 2026; [github.com/zhanglabtools/CAMEX](https://github.com/zhanglabtools/CAMEX), MIT) as a third homology-aware backend of the unified cross-species API added in #893.

CAMEX is a **heterogeneous GNN** that integrates and annotates scRNA-seq across species using the **many-to-many homolog graph** (not just 1:1 orthologs) and natively handles **>2 species at once** — a capability neither SAMap nor SATURN offers. (Surfaced by the post-#856 literature scan as the most wrappable newer method.)

## What's added

- **Vendored** under `omicverse/external/camex/` (not on PyPI; upstream pins `numpy<=1.24` / `scanpy<=1.9.3` / `pandas==1.5.3` / `numba==0.56.4`, incompatible with omicverse) with compat patches for the current env:
  - DGL ≥1.0: `NodeDataLoader` → `DataLoader` shim
  - pandas 2.x: fix 2-D column assignment in `_store_integration`/`_store_train`
  - lazy heavy imports (`scib`, `scanpy.external`) so `import omicverse.external.camex` stays light
- **Unified API**: `ov.single.CrossSpecies(..., method='camex')` / `cross_species_integrate(..., method='camex')`. `_fit_camex` builds the **many-to-many homology from BioMart** (`get_orthologs(orthology_type='all')`) linking the reference species to each other, then runs the vendored `Dataset → Trainer.integration()` pipeline, returning `obsm['X_CAMEX_Integration']`.

```python
# multi-species (>2) in one call
adata = ov.single.cross_species_integrate(
    [a_human, a_mouse, a_zebrafish], ['human','mouse','zebrafish'], method='camex')
```

## Verification

End-to-end on real frog+zebrafish via `CrossSpecies` (10 820 cells, GPU, ~5 min @ 100 epochs): cross-species label transfer **germ-layer 0.64 / cell-type 0.24**. Honest framing: CAMEX's edge is **multi-species + annotation transfer**, not 2-species distant-pair embedding quality — SATURN (0.86/0.62) remains best on that specific benchmark. The value here is the new multi-species / many-to-many-homology capability.

Tests: `tests/single/test_camex_vendored.py` (import + wiring, `importorskip` torch+dgl) — **7 passed** with the other backend tests. flake8 (E9,F63,F7) clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d71c908fbb4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.