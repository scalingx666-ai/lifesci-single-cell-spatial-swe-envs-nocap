# Issue

**Title:** All D-list transcripts have the same ID

## Description

This PR changes the transcript IDs of the D-list sequences in the de Bruijn graph, such that they all have the same ID. Otherwise, if a read aligns to more than one D-list sequence they will be masked out in the intersection.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9307adf896f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.