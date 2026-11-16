# Issue

**Title:** Visium HD workflow (& other fixes)

## Description

Changes:

- fix the seq-decon schematic png with thicker border
- fix bkg-datasets small description on Janesick breast cell type annotation source and chromium dimension
- merge in seq-workflow-vis-crc p2 subsetting
- add biblio.bib and new two dependencies to DESCRIPTION
- renamed crs-workflow-vishd to seq-workflow-vishd, with content drafted.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `df54f0ef02ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.