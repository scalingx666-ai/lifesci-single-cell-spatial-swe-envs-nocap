# Issue

**Title:** Update zUMIs.sh

## Description

This is a small optimization suggestion. There is no need to use `cat` to pipe `head` since `head` can read the file and stop when reaching the number of lines.

I tested this with a 24GB file, and this are the results:

```bash
$ time head -n 4000000 file.fastq > tmp.fastq
real	0m0.388s
user	0m0.252s
sys	0m0.136s
$ time cat file.fastq | head -n 4000000 > tmp2.fastq
real	0m0.426s
user	0m0.240s
sys	0m0.361s
$ diff tmp.fastq tmp2.fastq
```

At the same time this avoids using pipe and throwing a `cat: write error: Broken pipe` error.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60f7965c1ea9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.