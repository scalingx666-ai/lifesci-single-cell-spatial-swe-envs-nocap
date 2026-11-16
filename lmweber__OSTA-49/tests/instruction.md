# Issue

**Title:** initialize imaging-based ST part

## Description

- `img-quality-control`: basic QC on Xenium, some (FOV-based) QC on CosMx
- `img-clustering`: standard (transcription-based) clustering, `Banksy` (spatially aware), visual and PC-based exploration
- `img-neighbors`: `RANN` (basic k/fixed-radius NN searches), `imcRtools` (niche analysis), `hoodscanR` (co-localization) 
- also initializing (skeleton) chapters on spatial statistics, cell-cell communication, and sub-cellular analyses

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `497015d0bf7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.