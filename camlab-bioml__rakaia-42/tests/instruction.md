# Issue

**Title:** Dev (v0.2.0)

## Description

Summary of proposed changes: 

- more updates to panning/zooming to close #28 
- uirevision property on canvas to resolve #20 
- save preset values and selected channels across ROi switch.  
- Lazy loading of datasets from mcd makes data import and ROI analysis much faster
- UI adjustments:  
- Cap area statistics very far zoomed out:  
- Add error message modal on uploads:  
- Canvas zoom on fullscreen:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6799212fe256`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.