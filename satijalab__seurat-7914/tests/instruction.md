# Issue

**Title:** Highlight fix

## Description

Hi @Gesmira & Seurat Team,

This is PR addresses two issues:
First, addressing #7891.  I have added raster parameter to SetHighlight, and a check to change the pt.size returned if TRUE.

I have also made the fix mentioned in comments for PR #7842 which causes raster warning to accidentally be always displayed regardless of whether TRUE/FALSE is supplied.

Thanks again!
Best,
Sam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `99b9ded61e0c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.