# Issue

**Title:** feat(epi): add ov.epi epigenomics module + tutorial-epigenetics chapter

## Description

## Summary
Adds **`omicverse.epi` (`ov.epi`)** — a thin omicverse-flavoured bridge over the [epione](https://github.com/aristoteleo/epione) package, bringing **epigenomics** (single-cell ATAC-seq, footprinting, chromVAR motif activity, peak-to-gene linkage, and Hi-C) into omicverse. Every wrapper imports `epione` internally and delegates, so `import omicverse` stays light and epione is an optional dependency (lazy-loaded via the existing `_LAZY_MODULES` mechanism).

### `ov.epi` layout
- `pp` / `tl` / `pl` / `io` / `datasets` / `data` — curated wrappers (real signatures + docstrings, `import epione` inside each)
- `single` / `bulk` / `upstream` / `utils` — lazy passthroughs to the matching epione submodules
- Each submodule has a module-level `__getattr__` forwarding any uncurated name to epione, so the full surface stays reachable
- `'epi'` registered in `omicverse/__init__.py` `_LAZY_MODULES`

### Tutorials (submodule bump → omicverse-tutorials#feat/epigenetics-tutorials)
New `tutorial-epigenetics` chapter with **8 executed notebooks** (real baked outputs, run in conda `omicdev`):
1. scATAC preprocessing & QC
2. clustering, annotation & gene activity
3. chromVAR TF motif activity
4. peak-to-gene linkage (multiome)
5. marker peaks / differential accessibility
6. scRNA–scATAC integration & label transfer (~83% acc vs paired ground truth)
7. bulk Hi-C (contact maps, compartments, TADs)
8. single-cell Hi-C (imputation + cell-cycle embedding)

Tutorials 1–6 auto-download public 10x PBMC data via `ov.epi.datasets`; 7–8 read local `.cool`/`.scool` (provenance noted in-notebook).

## Local checks
- `flake8 --select=E9,F63,F7 omicverse/epi/` → 0
- all `ov.epi` submodules import cleanly
- isolated `sphinx-build -W` of the new chapter → build succeeded, 0 warnings

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30dd5c042c93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.