# Issue

**Title:** fix(cnv): save inferCNV coordinates and fastCNV scores

## Description

## Why
`RunCNV()` dropped chromosome coordinates when it saved inferCNV results. When a Seurat object also held a DecontX embedding, the fastCNV path could save that embedding as the CNV matrix.

## What changed
- Match inferCNV matrix rows to the supplied gene order by gene ID and save chromosome, start, and end.
- Read fastCNV matrices from `genomicScores` and report an error if that assay is missing.

## Scope
These changes affect how SCOP saves the results of these two methods. They leave the inference algorithms and heatmap rendering code unchanged.

## Verification
- Ran native inferCNV 1.23.0 on the bundled oligodendroglioma counts with a shuffled coordinate table. All 9,217 retained genes matched the native coordinates, the 184-cell matrix matched the native scores exactly, and the rendered heatmap placed every gene in the correct one of 22 chromosome groups.
- Ran native fastCNV 1.1.10 with a DecontX embedding present. The saved 56-by-40 matrix matched `genomicScores` exactly.
- Passed the CNV test file, including the coordinate alignment and matrix source regressions.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f8a9791297d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.