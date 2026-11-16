# Issue

**Title:** Remove orphaned GFFREAD_TRANSCRIPTOME local module

## Description

## Summary

- Remove the unused local `GFFREAD_TRANSCRIPTOME` module (`modules/local/gffread_transcriptome/`)
- Add a changelog entry under `Chore`

## Background

`GFFREAD_TRANSCRIPTOME` was added in April 2021 as part of the early DSL2 pipeline. It ran `gffread -F` on a GTF and genome FASTA to produce a transcriptome FASTA when users did not supply `--transcript_fasta`.

That output was needed for the **Alevin** path: the transcriptome FASTA was passed into `SALMON_INDEX` to build a Salmon index (gentrome with genome decoys) before quantification.

## Why it is no longer used

In August 2022, `SIMPLEAF_INDEX` replaced `SALMON_INDEX` for Alevin index building. Simpleaf can build the index directly from genome FASTA and GTF (`--gtf`), so the explicit transcriptome extraction step became redundant.

The module invocation was removed in commit `9fd3649`, but the module file was left behind. The orphaned `include` was finally dropped during the 2025 simpleaf subworkflow refactor (`fec1962`). The file has had no callers since 2022.

## Test plan

- [x] No workflow references to `GFFREAD_TRANSCRIPTOME` remain
- [ ] CI passes (no functional change expected)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40f076f916e7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.