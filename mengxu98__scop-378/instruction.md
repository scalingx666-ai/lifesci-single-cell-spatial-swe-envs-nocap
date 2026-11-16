# Issue

**Title:** fix(spatial): restore VisiumV2 coordinate axis order

## Description

Seurat's standard Read10X_Image() stores imagerow/imagecol positionally as VisiumV2 centroid x/y. This restores x=imagecol and y=imagerow for raw analysis and display coordinates while preserving explicit generic FOV x/y. Targeted spatial tests, Read10X-style smoke test, and pkgload::load_all(..., compile=FALSE) pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4f909f063733`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.