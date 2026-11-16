# Issue

**Title:** Add related packages to README, update bib entries, remove cellrank.org references

## Description

## Summary

Housekeeping PR with three changes:

### 1. Add "Related packages" section to README
Compact table listing 6 sibling packages (moscot, moslin, VeloVI, RegVelo, CellMapper, CellAnnotator) with links to docs and references. Notes scverse ecosystem membership.

### 2. Update references.bib
- **moscot** (`klein:23` → `klein:25`): updated from bioRxiv preprint to published *Nature* **638**, 1065–1075 (2025), with full 20-author list.
- **moslin** (`lange:23` → `lange:24`): updated from bioRxiv preprint to published *Genome Biology* **25** (2024).
- Added **VeloVI** (`gayoso:24`): *Nature Methods* **21**, 50–59 (2024).
- Added **RegVelo** (`wang:24`): *bioRxiv* (2024).
- Updated `:cite:` reference in `RealTimeKernel.from_moscot()` docstring.

### 3. Remove outdated cellrank.org references
- Replaced `cellrank.org` URLs with `cellrank.readthedocs.io/en/latest/`.
- Removed v1→v2 migration banner from Sphinx config and docs index.
- Renamed "Moving to CellRank 2" page to "Moving from v1 to v2".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0c23eaa743a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.