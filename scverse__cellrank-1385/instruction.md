# Issue

**Title:** docs: move to scverse-doc and adopt the shared scverse docs TOC

## Description

## Changes

* Switches the docs from furo to scverse-doc and groups the sidebar into Getting started, Guides, Reference and Project as agreed in scverse/scverse-doc#62, with the getting-started notebook as the quickstart.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7821af1ff26`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.