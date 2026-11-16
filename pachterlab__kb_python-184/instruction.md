# Issue

**Title:** Added flags to create genomebam file with kallisto bus

## Description

`kallisto bus` has the following optional options:
```
--genomebam               Project pseudoalignments to genome sorted BAM file
-g, --gtf                     GTF file for transcriptome information
                              (required for --genomebam)
-c, --chromosomes             Tab separated file with chromosome names and lengths
                              (optional for --genomebam, but recommended)
```

This PR adds parameters to `kb count` so that one can use the `--genomebam` flag as well as a gtf file and optionally a chromosomes file to output a .bam file. A test is added to make sure the functionality works as intended.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `14a18ef36a94`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.