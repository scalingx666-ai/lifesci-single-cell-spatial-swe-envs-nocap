# Issue

**Title:** Specify a whitelist when adding barcodes

## Description

Hello, following up issue #60 I've added the possibility to specify a whitelist to the `barcode` predicate. This may be useful if one doesn't want to create an extra fastq file containing the corrected barcodes, hence saving some disk space (also considering the fact it is recommended to use uncompressed fastqs).
If no whitelist is specified nothing changes. Otherwise one can supply either a whitelist from UMI-tools or a generic whitelist. In the first case it will be directly used to correct barcodes whenever possible, without checks. In the second case it will make use of of [UMI-tools API](https://umi-tools.readthedocs.io/en/latest/API.html#the-umiclusterer-class) and will correct barcodes on the fly.
If correction is made on the fly, an extra time will be needed to process data, much depending on the fastq size

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56f3693fc7ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.