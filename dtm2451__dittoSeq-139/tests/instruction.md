# Issue

**Title:** Update for ggplot2-v3 and other warnings

## Description

This PR makes various updates to keep up with changes in dependencies:
- Per ggplot2's deprecation of `aes_string()`, adjusts how mappings are built to align with current recommendations.
- Per ggplot2's update to not autoconvert 'size' aesthetic names to use 'linewidth' without a warning, changes all relevant spots to use 'linewidth' directly.
- Per Seurat's deprecation of the `slot` argument of `SeuratObject::GetAssayData()`, switches to grabbing via `object[[assay]][slot]` conditional on the Seurat version being 5+.  (This same method would likely work the same for earlier versions too, but why fix what's not broken!  Edit: It DOES NOT work for Seurat v4.3.0, so the split in methodology introduced here is going to stay -- not changing everywhere was the right intuition!)

The PR does not address warnings that can currently come from `dittoScatterHex()` and `dittoDimHex()` when mixing a `color.var` with faceting, about 'the z aesthetic getting dropped during statistical transformation'.  The fault here lies in the `ggplot.multistats` package, and is fixed with the version available from GitHub, just not the one currently in CRAN.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfff82e7d08b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.