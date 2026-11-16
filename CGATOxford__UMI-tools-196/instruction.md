# Issue

**Title:** renames --whole-contig option to --buffer-whole-contig and updates doc.

## Description

The naming of this option causes confusions since the introduction (by me) of very similar sounding `--per-contig` option. E.g . Hopefully, the renaming will resolve this confusion

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9cdd53e5f11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.