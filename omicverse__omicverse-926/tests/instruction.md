# Issue

**Title:** release: omicverse 2.3.0

## Description

Two changes: the version, and the submodule pointer.

## Version — 2.3.0, not 2.2.5

Twenty-four commits since 2.2.4, of which twenty-one are user-facing, and **eight modules are new**. A patch bump would understate that.

| | |
|---|---|
| `ov.flow` | FCS reading, display transforms, the gating strategy tree, and Gating-ML that validates |
| `ov.mol` | GPU molecular dynamics — simulate, analyse, MM-GBSA |
| `ov.pl` | table-first statistical plots with an AnnData adapter; clinical statistics and publication figure assembly |
| `ov.alignment` | homology search (DIAMOND/BLAST+) and Sanger `.ab1` verification |
| `ov.space` | SPATA2-style coordinate utilities; the arrangement layer (`nb` / `niche` / `geom`); a Stereo-seq reader |
| `ov.synbio` | the D-segment gaps closed — reconstruction, omics→GEM, manufacturability, biosecurity |

It also carries user-visible corrections that should not wait for another cycle: roughly forty synbio defects that produced plausible wrong numbers, Gating-ML output that was not valid Gating-ML, CopyKAT failing silently when its genome tables are missing, a `[synbio]` extra that could not be installed, and the rpy2 mclust bridge replaced by the pure-Python pymclustR backend.

## Submodule — ten commits behind

`omicverse_guide` was pinned at `8863da9c` (the `ov.flow` tutorial series) while `omicverse-tutorials` main had moved to `63c17868`. Everything merged in between — the MD tutorial, both synbio sets, four plotting tutorials, AIRR, SPATA2, and the spatial arrangement tutorials — was absent.

Documentation builds read the tutorials through this pointer, so leaving it behind kept all of that material off the docs site regardless of it being merged.

Release notes: omicverse-tutorials#TBD, which also fills in the 2.2.4 entry that was never written.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8985ccf915b4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.