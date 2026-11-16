# Issue

**Title:** Store multiple gene names on the worker side.

## Description

I now pass a dictionary of different namespaces for the genes to the main thread. This needs the corresponding UI change in the marker table to allow choosing between these different namespaces.

This will ultimately enable application of regexes during the QC step.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bd7b08f47cdb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.