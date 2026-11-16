# Issue

**Title:** Optionally use igzip for decompression of gzipped files.

## Description

igzip (https://github.com/intel/isa-l/) is quite a bit faster than standard gzip/pigz for decompressing gzipped files.

Total runtime might not be that much faster with igzip as in most cases igzip will only consume around 20% CPU as other commands in the pipeline can't keep up. But it lowers the total amount of CPU used by TrimGalore.

cutadapt also uses python-isal/igzip under the hood via xopen to read FASTQ files.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e4fb81ff4adf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.