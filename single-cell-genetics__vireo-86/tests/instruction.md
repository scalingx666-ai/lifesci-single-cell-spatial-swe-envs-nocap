# Issue

**Title:** Add all used FORMAT tags when writing VCF files.

## Description

Add a proper VCF header to "cellSNP.base.vcf.gz" so other tools can work with it.

Before this patch Picard couldn't work with the "GT_donors.vireo.vcf.gz" file at all as it requires complete VCF header by default and BCFtools would emit warnings about FORMAT fields not defined in the header and assuming "Type=String" instead of the correct type.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3926aa1023fe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.