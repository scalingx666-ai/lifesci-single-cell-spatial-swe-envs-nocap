# Issue

**Title:** Release 2.0.4

## Description

What's new in v2.0.4:

- Fix bug caused by mixing up (i, j) and (x, y) coordinate systems in BioFormatsBackend (#278)
- Add option to not normalize image in `BioFormatsBackend.extract_region()` (#279)
- Fix logic when inferring correct backend to use from file path which was failing on paths containing periods (#284)
- Fix bug to correctly pass `image_resolution` argument to Mesmer model (#286)
- Fix outdated url for PanNuke dataset (#287) @Yu-AnChen
- Fix GitHub Actions configuration which was causing testing suite to hang (#289)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1010b3a870cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.