# Issue

**Title:** Add tagtorg command

## Description

Here is the implementation of the feature briefly described in #8.

The `tagtorg` command allows replacing RG tags with read tag-specific tags. This is done in a single pass and without creating files other than the output file.

I have tried to follow the conventions in the code as much as possible, but I broke with one point of sinto code style and coded the command to follow the UNIX convention of being able to read data from stdin and output results to stdout.  I allow the specification of a dash `-` to indicate this. 

I use pysam to parse the input and write the output data. Pysam allows reading of SAM and BAM formatted data and allows the output of SAM, compressed BAM, and uncompressed BAM. As these features come for free with pysam, this command also provides them. In practice I find a substantial speedup when I output uncompressed BAM to stdout and let samtools compress it in a later stage of a (UNIX) pipeline.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `367ba12f5254`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.