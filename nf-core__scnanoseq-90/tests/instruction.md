# Issue

**Title:** Swapping out samtools view for a custom script to split bams by contig.

## Description

This change will modify the logic we use to split transcriptome aligned bams when using umitools.

The current logic uses samtools_view to split the bam. In order to split the bam, it would print the mappings to split to the commandline, because the mappings were all transcripts on a specific chromosome, this could result in an issue where there were too many strings printed to the commandline, crashing the pipeline.

This PR changes that logic to instead use a custom python script to be able to do this same behavior without printing the transcripts to the commandline

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc8db61b7dc1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.