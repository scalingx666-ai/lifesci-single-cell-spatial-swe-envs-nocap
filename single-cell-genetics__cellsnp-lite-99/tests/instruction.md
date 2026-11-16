# Issue

**Title:** Add a proper VCF header to "cellSNP.base.vcf.gz".

## Description

Add a proper VCF header to "cellSNP.base.vcf.gz" so other tools can work with it.

Before this patch Picard couldn't work with the "cellSNP.base.vcf.gz" file at all as it requires complete VCF header by default and BCFtools would emit warnings about INOF fields not defined in the header and assuming "Type=String" instead of "Number=1".

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6f9a6731bcb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.