# Issue

**Title:** release: omicverse 2.2.4

## Description

Bump version `2.2.4rc1` → `2.2.4` for the 2.2.4 release. Tagging `v2.2.4` after merge triggers the PyPI publish.

Highlights since v2.2.3 (66 commits): the new **`ov.synbio`** three-layer synthetic-biology module (metabolism / protein·enzyme / DNA) plus its advanced-SOTA layer (LinearDesign, Boltz-2, RFdiffusion de-novo binders, PrimeDesign, dynamic FBA, minimal cut sets, SBOL, evaluate_design scorecard), cross-species integration (orthologs + SAMap + SATURN), Seurat RPCA integration, and GPU/perf fixes in pp (sccomposite / scdblfinder / doubletfinder).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29b9cb69d985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.