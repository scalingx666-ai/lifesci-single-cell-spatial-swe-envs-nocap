# Issue

**Title:** Dev (v0.3.0)

## Description

## [0.3.0] - 2023-07-10

### Added

- first draft of zoomed in coordinate navigation #26
- add ability to add the pixel intensity values to the hover template #19
- percentile scaling #22 #45

### Fixed

- proper pixel blending for overlapping pixels
- better pixel scaling (linear from lower to upper bound)
- callback separation for speed improvements
- remove dcc.Stores from dcc.Loading by default to improve app smoothness

### Changed

- convert the pixel intensity changer to a range slider instead of box on the histogram

### Removed

- local dash diskcache background manager (conflict with pickle on certain Windows machines)

-  
-  
-  
-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eae9ab318046`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.