# Issue

**Title:** docs: move to scverse-doc and adopt the shared scverse docs TOC

## Description

Switches the docs from the scanpydoc theme to scverse-doc and groups the sidebar into Getting started, Guides, Reference and Project as agreed in scverse/scverse-doc#62, with the basic usage notebook as the quickstart.
liana's crimson and turquoise reach the docs once scverse/scverse.github.io#380 and a scverse-doc release carry them; until then the docs use the scverse blue.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3140d5c97634`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.