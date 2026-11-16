# Issue

**Title:** Create `dittoDotPlot()`

## Description

Creates a ditto-equivalent function for Seurat's `DotPlot()` and scater's `plotDots()` functions. The dot plot type allows compact plotting of per-grouping (typically clusters) summaries for multiple features.

![image](https://user-images.githubusercontent.com/38870347/93011922-fd5a5a80-f54f-11ea-913a-9194f0069295.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ca360d4b7ff`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.