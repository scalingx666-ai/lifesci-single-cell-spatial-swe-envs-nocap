# Issue

**Title:** Fix FigShare download URLs

## Description

FigShare changed their URL format. The old format (`figshare.com/ndownloader/files/...`) now returns a 202 WAF challenge instead of the file. The new format (`ndownloader.figshare.com/files/...`) returns a proper 302 redirect to S3.

This updates all dataset download URLs in `datasets.py` to the new format.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b3225c86fa8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.