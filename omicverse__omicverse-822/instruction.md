# Issue

**Title:** fix+feat(cnv): heatmap chromosome tiling, p/q arm split, infercnv phase2/3 + platform cutoff guard

## Description

## Summary
Fixes two `ov.pl.cnv_heatmap` rendering bugs, adds optional **p/q arm splitting**, surfaces the inferCNV **phase 2/3** outputs, and adds a **platform/cutoff guard** to `ov.single.CNV`.

## Bug fixes (`ov.pl.cnv_heatmap`)
- **Chromosome tiling**: `_build_chr_segments` used a tautological min/max-envelope "contiguous" check, so an interleaved non-standard scaffold left an uncovered hole — a chromosome past the gap rendered only partially / shifted to one side. Now kept columns are compacted via a mask and segments rebase to tile `[0, width)` (a `slice`/view is returned when nothing is dropped).
- **`NameError`**: the matplotlib group-divider branch referenced an undefined `primary` instead of the `groupby` parameter (crashed `backend='matplotlib'` + `groupby=`). Fixed.

## New: p/q arm split (`split_arms=True`)
- Columns stay grouped by **chromosome** (thin separator between chromosomes, original style); a centromere-aware **p/q colour band** marks the arm boundary *inside* each chromosome (the two arms render contiguously — no gap).
- Centromere coords vendored from **UCSC cytoBand** (hg38/GRCh38, hg19/GRCh37) under `pl/_data/` (+ package-data). Unknown/non-human genome → arms silently skipped (whole chromosomes drawn).
- Needs `adata.uns['cnv']['bin_meta']` (per-bin genomic coords) — see **dependency** below; falls back gracefully if absent.
- Backend note (honest): the **marsilea** backend draws the p/q colour band; the **matplotlib** backend marks the centromere with a dotted line + tiny `p`/`q` labels on the ideogram.

## New: inferCNV phase 2/3 surfacing + docs (`ov.single.CNV`)
- Documents that `run(..., HMM=True)` runs pyinfercnv phase 2/3 and writes `obs['cnv_subcluster']`, `obsm['X_cnv_hmm_states']`, `uns['cnv']['cnv_regions']` (plottable via `groupby='cnv_subcluster'`).

## ⚠️ Breaking: platform/cutoff guard for inferCNV
`ov.single.CNV(method='infercnv').run(...)` now **requires** `platform=` (`'10x'`→cutoff 0.1, `'smartseq2'`→1.0) **or** an explicit `cutoff=`, else raises `ValueError`. Rationale: the gene-filter cutoff is platform-dependent and the previous silent default (1.0, the SmartSeq2 value) over-filters 10x data — it drops ~3/4 of bins, producing a visibly over-smoothed heatmap. Migration: add `platform='10x'` (or your platform) to existing `run()` calls. CopyKAT is unaffected.

## Dependency
Arm splitting for the inferCNV backend needs `pyinfercnv` with the new `bin_meta` field (omicverse/py-inferCNV#4). Without it, `split_arms=True` falls back to whole chromosomes (no error). CopyKAT already provides `bin_meta`.

## Tests
`tests/pl/test_cnv_heatmap.py` (tiling invariant, centromere/arm split, view-slice, both-backend render) and `tests/single/test_cnv_platform.py` (platform guard). 14 pass against omicverse 2.2.0; end-to-end validated on a real 10x dataset (phase 1/2/3 + both plot backends). Independently code-reviewed (Codex).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f096ef958f94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.