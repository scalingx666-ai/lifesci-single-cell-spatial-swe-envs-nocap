# Issue

**Title:** Iupac extension

## Description

I downloaded genome GRCh38 through genomepy:

```
genome url: https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/405/GCF_000001405.26_GRCh38/GCF_000001405.26_GRCh38_genomic.fna.gz
annotation url: https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/001/405/GCF_000001405.26_GRCh38/GCF_000001405.26_GRCh38_genomic.gff.gz
```

When I run kb ref on this I get the error that R is not in BASEPAIRS.

I updated (and renamed) BASEPAIRS/COMPLEMENT to allow all IUPAC codes. My guess would be that kallisto can just work with this right? I'll make sure to test this.

complement cheatsheet I used:

http://arep.med.harvard.edu/labgc/adnan/projects/Utilities/revcomp.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `911f1846d4d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.