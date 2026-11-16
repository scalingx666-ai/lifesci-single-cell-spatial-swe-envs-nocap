# Issue

**Title:** Fixing 'Argument list too long' error

## Description

The following error occurred when running the `test_full` profile:

```
.command.sh: line 3: /usr/local/bin/samtools: Argument list too long
```

This change will modify the logic we use to split transcriptome aligned bams when using umitools.

The current logic uses samtools_view to split the bam. In order to split the bam, it would print the mappings to split to the commandline, because the mappings were all transcripts on a specific chromosome, this could result in an issue where there were too many strings printed to the commandline, crashing the pipeline.

This PR changes that logic to instead use a custom python script to be able to do this same behavior without printing the transcripts to the commandline

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a6aade735c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.