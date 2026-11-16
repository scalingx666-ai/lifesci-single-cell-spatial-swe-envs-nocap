# Issue

**Title:** Dev

## Description

- add uuid for unique session tagging for I/O
- modify parser to parse tiffs as either multi or single page based on page length (no longer restricted by the file extension name)
- update to accept multiple experiment uploads at once
- change download behavior to only when the download button is selected, and not every time the canvas or blend dictionary is modified
- add font awesome icon to fullscreen button

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d686f7fda700`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.