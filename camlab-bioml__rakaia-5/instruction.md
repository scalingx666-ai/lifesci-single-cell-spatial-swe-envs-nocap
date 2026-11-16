# Issue

**Title:** Speedup render

## Description

- Add channel expression information on zoom and rectangle draw
- Speed up rendering the re-coloured channels using native numpy array operations
- Cache processed channels to make blending much faster
- Use resized thumbnails in gallery to speed up rendering
- Add first prototype of adding legend to the plot
- increase size of possible uploads with du-uploader

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28240da54c23`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.