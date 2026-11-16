# Issue

**Title:** docs: move to scverse-doc and adopt the shared scverse docs TOC

## Description

Switches the docs from sphinx-book-theme to scverse-doc and groups the sidebar into Getting started, Guides, Reference and Project as agreed in scverse/scverse-doc#62, with new installation, quickstart and citation pages.
decoupler has no brand colours on the scverse website yet, so the docs use the scverse blue until the website and scverse-doc pick them up.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27a1be7c75d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.