# Issue

**Title:** updates gettag method to support 10X UMI tag encoding

## Description

10X long ranger pipelines add a tag with the UMI (BX) but this is also appended with the 'GEM' group, e.g
AGAGAGAGTA-1

Quoting from: https://support.10xgenomics.com/genome-exome/software/pipelines/latest/output/bam

_'This number denotes what we call a GEM group, and is used to virtualize barcodes in order to achieve a higher effective barcode diversity when combining samples generated from separate GEM chip channel runs. Normally, this number will be "1" across all barcodes when analyzing a sample generated from a single GEM chip channel. It can either be left in place and treated as part of a unique barcode identifier, or explicitly parsed out to leave only the barcode sequence itself.'_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ef816341ef4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.