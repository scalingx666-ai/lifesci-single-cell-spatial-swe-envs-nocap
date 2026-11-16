# Issue

**Title:** updated annot arguments for cellxgene v 0.15 & added option for backed mode.

## Description

This PR updates cellxgene to use the latest release from cellxgene in which annotations are enabled by default. 

It also adds the option to load the data in file-backed mode which significantly reduces loading time as the data is not fully loaded into memory. 

**NOTE**: I could not fully test the annotation mode as I did not find the way to specify the `annotation_file`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11bbc1aba850`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.