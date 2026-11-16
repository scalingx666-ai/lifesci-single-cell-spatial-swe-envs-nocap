# Issue

**Title:** Fix `--input` help text to point to scrnaseq samplesheet docs

## Description

It seems like a long time ago, a reference to the nf-core/rnaseq docs creeped into our documentation of the `input` param. Was pointed out by a user in [this slack thread](https://nfcore.slack.com/archives/CHN5BV5DW/p1783608984580569). This PR replaces the reference with the proper one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `96dadeb2088a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.