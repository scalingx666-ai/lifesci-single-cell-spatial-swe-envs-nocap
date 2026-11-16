# Issue

**Title:** Read10x updates

## Description

All changes modify `read10xVisiumWrapper()` to allow finding and importing the reference GTF properly, namely when `reference_gtf` is not specified. In particular:
- Correctly find the reference GTF for recent versions of spaceranger, which have a differently organized `web_summary.html` file
- Support importing GTF files that are gzipped, which occurs for recent reference genomes (such as those from 2024)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c82c789d8538`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.