# Issue

**Title:** docs: adopt the shared scverse docs TOC

## Description

Groups the docs sidebar into Getting started, Guides, Reference and Project as agreed in scverse/scverse-doc#62, with the basic workflow notebook as the quickstart and a new citation page, and takes both accents from scverse-doc 0.4's registry instead of hard-coding them.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1edfbc80db00`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.